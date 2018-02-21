---
title: Object Data
category: Puko Object Data
order: 1
---

> WAING: THIS FEATURE UNDER DEVELOPMENT ON dev-master BRANCH

> Coming Soon in version 1.1.3

Puko framework memanfaatkan instansiasi sebuah object untuk melakukan proses CRUD.
Fitur ini dinamakan Object Data. Untuk dapat melihat bagaimana Object Data ini bekerja, anda dapat melihat contoh sintaks berikut:

```php
$bibit = new bibit_pohon();
$bibit->harga = 35000;
$bibit->jenis_pohon = "Mangga Apel";
$bibit->jumlah = 5;
$bibit->ket = "Dari cangkokan super";
$bibit->save();
```

Dari potongan kode di atas kita dapat mengetahui bahwa:
* **bibit_pohon** adalah intansiasi sebuah kelas.
* **bibit_pohon** mempunyai property berupa harga, jenis_pohon, jumlah dan ket.
* **bibit_pohon** juga melakukan proses penyimpanan data dengan pemangglan fungsi save().

Jika anda penasaran bagaimana bentuk dari kelas bibit_pohon itu sendiri, maka inilah kodenya:

```php
<?php
namespace plugins\model;

use pukoframework\pda\DBI;
use pukoframework\pda\Model;

/**
 * #Table bibit_pohon
 * #PrimaryKey id
 */
class bibit_pohon extends Model
{
    
    /**
     * #Column id int(10)
     */
    var $id = null;

    /**
     * #Column jenis_pohon varchar(45)
     */
    var $jenis_pohon = null;

    /**
     * #Column jumlah int(5)
     */
    var $jumlah = null;

    /**
     * #Column harga int(8)
     */
    var $harga = null;

    /**
     * #Column ket varchar(225)
     */
    var $ket = null;

    public static function Create($data)
    {
        return DBI::Prepare('bibit_pohon')->Save($data);
    }

    public static function Update($where, $data)
    {
        return DBI::Prepare('bibit_pohon')->Update($where, $data);
    }

    public static function GetAll()
    {
        return DBI::Prepare('SELECT * FROM bibit_pohon')->GetData();
    }

}
```

> Perhatian: anda tidak perlu membuat kelas ini karena sudah ter-generate otomatis dalam scaffolding **php puko setup db**

Bagian pertama yang perlu diperhatikan adalah deklarasi kelas:

```php
/**
 * #Table bibit_pohon
 * #PrimaryKey id
 */
class bibit_pohon extends Model
```

Dimana terdapat *#Table bibit_pohon* dan *#PrimaryKey id* yang menunjukan bahwa kelas tersebut terkoneksi dengan sebuah tabel di database
dengan nama tabel **bibit_pohon** dan mempunyai primary key dengan nama kolom **id**. Saat proses scaffolding puko melakukan pembacaan struktr data hingga ke tingkat kolom.

Kemudian kita juga dapat memperhatikan property yang terbentuk di dalam kelas:

```php
/**
 * #Column id int(10)
 */
var $id = null;
```

Penggunaan *#Column id int(10)* membuat puko framework mengetahui bahwa variabel itu terkait dengan kolom bernama sama di dalam database.

Lalu apa yang menarik dengan metode seperti ini?
* Kita dapat melakukan proses CRUD tanpa menuliskan query SQL.
* Membuat kolom database Code Completion-able pada kode PHP.
* Menghasilkan sintaks yang rapih dan mudah.

Terima kasih sudah menyempatkan diri mencoba framework ini. Jika ada masalah atau ide menarik silahkan mengirim sebuah issue pada
repositori puko framework di [sini](https://github.com/Velliz/pukoframework/issues)

> TODO: Table Relation Feature.