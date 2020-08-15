---
title: Model
category: Basics
order: 3
---

Let's get to know about model. The (M) layer of puko framework HMVC pattern.
This part of puko has responsible to connecting your app with a database 
or multiple database for Create, Read, Update and Delete operations.
Database in puko handled by the DataBase Interface (DBI) singleton objects.

But, before that, we need setup a database connections. To summarize the process we often using `pukoconsole` command:

```
php puko setup db
```

Items asked:

|Items|Description|Examples|
|---|---|---|
|Database Type|only supports MySQL for now|mysql|
|Hostname|Databaase IP address|localhost|
|Port|Databaase port address|3306|
|Schema Name|Schema name as identifier for multiple database|primary|
|Database Name|Name of databases|inventory|
|Username|User databases|root|
|Password|Paassword databases|******|

> At the end wizard is asking for another connection you can answer with y/n

What this process means?

Puko will save the connection setting in `config/database.php` file 
and generate corresponding PHP class model as **data object wiring** with your database model.
Those files generated and saved in `plugins/model/<schema>` directory.

> That file should not be modified

So, why we need **data object wiring**?

At concept level, data object wiring inspired by Data Access Object (DAO) patterns 
but only implement the wiring mechanism to keep it small and simple.
And because we usually don't remember clearly the column on database entity. 
So with object wiring you now have clues about your column on the database in case you forget.
Especially when used with good IDE, those tools can provide auto-completions trough your data.
Enough theory, let's see it in action.

Assumed you have basic knowledge on MySQL and have a database table `inventory` and you already done executing setup db command above.
This is example of what inside table `inventory`:

|id|name|created|descriptions|
|---|---|---|---|
|1|Chair|2020-08-15|Minimalist chair made from pine woods|
|2|Laptop|2020-08-16|Gaming notebooks with core i7 and RTX2070 Max-Q|

> Alert: tables name must only contain letters without special character or space due to limitations of php class name rules.

Create or save operations:

```php
$inventory = new plugins\model\primary\inventory();
$inventory->id = $_POST['id'];
$inventory->name = $_POST['name'];
$inventory->created = date('Y-m-d H:i:s');
$inventory->descriptions = $_POST['descriptions'];

$inventory->save();
```

Read operations:

```php
$inventory = new plugins\model\primary\inventory(1);

echo (array) $inventory;
```

Update or modify operations:

```php
$inventory = new plugins\model\primary\inventory(1);
$inventory->id = $_POST['id'];
$inventory->name = $_POST['name'];
$inventory->created = date('Y-m-d H:i:s');
$inventory->descriptions = $_POST['descriptions'];

$inventory->modify();
```

Delete or remove operations:

```php
$inventory = new plugins\model\primary\inventory(1);

$inventory->remove();
```

Get all data:

```php
$all = plugins\model\primary\inventory::GetAll();
```

As you can see. Basic CRUD operations is simple and don't need to use any manual typed SQL query.

---

> The DataBase Interface (DBI) in puko framework for now only support MySQL and MariaDB. 

---

**Alternative**

You can also make database operation trough DBI without using `pukoconsole` command.
We call it old way methods. The PHP class/file required must located in outer model folder.

> TODOC

```php
$data['mahasiswa'] = Mahasiswa::GetAll();
```

Untuk melakukan proses simpan data, anda dapat menggunakan **Create()**.

```php
$id_mahasiswa = Mahasiswa::Create(array(
    'Nama' => 'Didit Velliz',
    'Jurusan' => 'Informatika',
    'IPK' => 4.00,
    ...
));
```

Untuk melakukan proses update data, anda dapat menggunakan **Update()**.

```php
$id_mahasiswa = Mahasiswa::Update(array('Id' => $id_mahasiswa), array(
    'Nama' => 'Didit Velliz',
    'Jurusan' => 'Informatika',
    'IPK' => 4.00,
    ...
));
```

> Perhatian: anda dapat menggunakan petunjuk kolom lain untuk melakukan update data.

```php
$id_mahasiswa = Mahasiswa::Update(array('Jurusan' => 'Informatika'), array(
    'Nama' => 'Didit Velliz',
    'Jurusan' => 'Informatika',
    'IPK' => 4.00,
    ...
));
```

|Fungsi|Parameter|Parameter Kembalian|
|Save()|array|**ID** atau **false**|
|Update()|array dan array|**true** atau **false**|
|GetData()|String query|**array** atau **null**|
|Delete()|array|**true** atau **false**|

Anda juga dapat membuat model dari turunan kelas tersebut.

```php
class Perwalian extends Mahasiswa {
```

> Perhatian: semua kelas model harus diletakan di dalam folder model yang telah disediakan.

Berikut ini adalah contoh lengkap model sederhana yang bisa anda buat.

```php
namespace model;

use pukoframework\pda\DBI;

class Perwalian extends Mahasiswa {

    public static function RataRataIPK() {
        $sql = "SELECT AVG(IPK) FROM Mahasiswa;";
        $data = DBI::Prepare($sql)->GetData();
        
        return $data;
    }
    
    public static function GetIPK($id_mahasiswa) {
        $sql = "SELECT IPK FROM Mahasiswa WHERE Id = @1;";
        $data = DBI::Prepare($sql)->FirstRow($id_mahasiswa);
        
        return $data;
    }

    public static function ResetIPK($id_mahasiswa) {
        $sql = "UPDATE Mahasiswa SET IPK = 0.0 WHERE Id = @1;";
        $data = DBI::Prepare($sql)->Run($id_mahasiswa);
        
        return $data;
    }        
}
```

Jika membuat turunan model, anda dapat memanfaatkan kelas static bernama DBI untuk melakukan manipulasi data. 
Contoh pengunaan DBI dapat anda lihat pada contoh lengkap model di atas yang menggunakan tiga cara pemakaian DBI.

```php
DBI::Prepare($sql)->GetData();
```

**GetData()** digunakan untuk mengambil keseluruhan data dari query yang dijalankan. Data yang dikembalikan berupa array berindeks.
Selain itu, kita juga bisa menyisipkan parameter secara bebas melalui parameter masukan dari **GetData()** itu sendiri sesuai dengan
jumlah parameter yang di definisikan di dalam query.

```php
$sql = "SELECT * FROM Mahasiswa WHERE Id = @1;";
DBI::Prepare($sql)->GetData($Id);
```

```php
$sql = "SELECT * FROM Mahasiswa WHERE Id = @1 AND IPK = @2;";
DBI::Prepare($sql)->GetData($Id, $IPK);
```

```php
$sql = "SELECT * FROM Mahasiswa WHERE Id = @1 AND IPK = @2 AND Jurusan = @3;";
DBI::Prepare($sql)->GetData($Id, $IPK, $Jurusan);
```

Terdapat juga penggunaan **FirstRow()** untuk mengambil hanya baris pertama saja dari data terpilih dengan kembalian berupa array tak berindeks.

```php
$sql = "SELECT * FROM Mahasiswa WHERE Id = @1 LIMIT 1;";
DBI::Prepare($sql)->FirstRow();
```

Terdapat juga penggunaan **Run()** untuk mengirim query saja. Biasanya digunakan untuk eksekusi stored procedure dan *query sql* selain *select*.

```php
$sql = "UPDATE Mahasiswa SET IPK = 0.0 WHERE Id = @1;";
DBI::Prepare($sql)->Run();
```

Anda juga dapat melihat *file* konfigurasi yang disimpan dari proses *Scaffolding* pada *file* config/database.php dengan format file berikut.
 
```php
return array(
    'dbType' => 'mysql',
    'host' => 'localhost',
    'user' => 'root',
    'pass' => '',
    'dbName' => '',
    'port' => 3306
);
```