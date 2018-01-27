---
title: Model
category: Basics
order: 3
---

Untuk dapat menggunakan model, anda harus terlebih dahulu memiliki *base model* yang disediakan dalam *Scaffolding*.
Sintaks berikut dapat anda jalankan untuk membuat sebuah model.

```text
php puko setup db
```

> Perhatian: sampai saat ini *Puko* framework baru mendukung secara penuh database MySQL & MariaDB.

Setelah menekan enter, anda akan dibimbing untuk melengkapi konfigurasi database dengan isian sebagai berikut.

```text
host name     : ...
```

Dapat di isi dengan *Alamat IP* lokasi mesin database, secara default kita bisa mengisikan **localhost**.

```text
host port     : ...
```

Dapat di isi dengan *port* database, secara default kita bisa mengisikan **3306**.

```text
username      : ...
```

Dapat di isi dengan user database, secara default kita bisa mengisikan **root**.

```text
password      : ...
```

Dapat di isi dengan password database, secara default kita bisa mengosongkannya.

```text
database name : ...
```

Dapat di isi dengan nama skema database.

> Perhatian: nama tabel tidak boleh diawali dengan angka serta nama tabel tidak diperbolehkan mengandung spasi.

Setelah selesai, jika konfigurasi yang di masukan benar. Maka akan ada informasi model apa saja yang berhasil di buat.
Anda bisa mengaksesnya melalui intansiasi objek sesuai dengan nama tabelnya. 
Untuk nama tabel Mahasiswa, maka anda dapat memanggil **GetAll()** untuk mengambil keseluruhan datanya.

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