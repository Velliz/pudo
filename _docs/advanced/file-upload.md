---
title: File Uploading
category: Advanced
order: 1
---

*Puko Framework* menyediakan utility untuk melakukan proses upload file. 
Kamu bisa langsung melakukan unggahan kamu menggunakan form seperti contoh berikut:

```html
<form action="" method="POST" enctype="multipart/form-data">
    <input type-"file" name="file_picture" required/>
</form>
```

penamaan input name harus mengandung kata **file_** lalu disambungkan dengan kata bebas lain 
agar puko dapat mendeteksi file tersebut adalah data unggahan.
Pada contoh ini kita menggunakan kata file_picture.

Untuk dapat menyimpan file tersebut kedalam database dengan tipe data BLOB kamu bisa langsung menggunakan perintah insert berikut.

```php
$input = array(
    'filedata' => $_FILES['file_picture']['tmp_name'],
    ...
);

DBI::Prepare('namatabel')->Save($input);

DBI::Prepare('namatabel')->Update(array('id' => 1), $input);
```

selain itu, ada kondisi dimana data yang kamu punya pada variable 'filedata' adalah string binary.
untuk menyimpan file binary diluar variable $_FILES kamu bisa menggunakan tambahan variable yaitu binary output dengan nilai 'true'.

```php
DBI::Prepare('namatabel')->Save($input, true);

DBI::Prepare('namatabel')->Update($where, $data, true);
```

TODO
