---
title: Model
category: basics
order: 3
---

Untuk dapat menggunakan database kamu harus menyiapkan konfigurasi terlebih dahulu yang dapat kamu temukan pada **config/database.php**
Kamu bisa menyesuaikannya dengan pengaturan masing-masing komputer yang digunakan.

```php
<?php

return array(
    'dbType' => 'mysql',
    'host' => 'localhost',
    'user' => 'root',
    'pass' => '',
    'dbName' => '',
    'port' => 3306
);
```

Setelah beres, kamu dapat membuat **model class** dengan cara meletakannya dalam folder bernama **model**.
Berikut ini adalah contoh model class sederhana yang bisa kamu buat.
Setiap kelas model wajib dinamai dengan huruf kecil semua. Kemudian model wajib menggunakan

```php
<?php

namespace model;

use pukoframework\pda\DBI;
```

Kemudian, untuk melakukan operasi CRUD kamu bisa memanfaatkan kelas static bernama DBI. Contoh pengunaan DBI

```php
DBI::Prepare('member');
DBI::Prepare('select * from member');
```

Untuk query Insert atau Update, kamu bisa memasukan nama tabel atau memasukan query select seperti contoh diatas.
Untuk lebih jelasnya, yuk lihat contoh sebuah kelas model dengan CRUD method didalamnya dibawah ini.

```php
<?php

namespace model;

use pukoframework\pda\DBI;

class yourdb
{
    public static function create($dataMember)
    {
        return DBI::Prepare('member')->Save($dataMember);
    }

    public static function read()
    {
        return DBI::Prepare('select * from member')->GetData();
    }

    public static function update($dataMember)
    {
        $whereClause = array('ID' => 1);
        return DBI::Prepare('member')->Update($whereClause, $dataMember);
    }

    public static function delete($dataMember)
    {
        $whereClause = array('ID' => 1);
        return DBI::Prepare('member')->Delete($whereClause);
    }
}
```

|Fungsi|Parameter|Parameter Kembalian|
|Save()|array|**ID** atau **false**|
|Update()|array dan array|**true** atau **false**|
|GetData()|String query|**array** atau **null**|
|Delete()|array|**true** atau **false**|

Berikut ini contoh terinci penggunaan parameter dengan Save();

```php
public static function create()
{
    $dataMember = array(
        'NIK' => '1266409',
        'Nama' => 'Didit Velliz',
        'Usia' => 22,
    );
    $hasil = DBI::Prepare('member')->Save($dataMember);
}
```

Berikut ini contoh terinci penggunaan parameter dengan Update();

```php
public static function update()
{
    $dataMember = array(
        'ID' => 1,
        'NIK' => '1266409',
        'Nama' => 'Didit Velliz',
        'Usia' => 22,
    );
    $whereClause = array('ID' => 1);
    $hasil = DBI::Prepare('member')->Update($whereClause, $dataMember);
}
```