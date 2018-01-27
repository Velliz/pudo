---
title: File Uploading
category: Advanced
order: 1
---

*Puko* menyediakan fasilitas untuk memudahkan proses upload file. 
Anda bisa langsung melakukan unggahan file menggunakan form html seperti contoh berikut.

```html
<form action="" method="POST" enctype="multipart/form-data">
    <input type="file" name="file_berkas" />
</form>
```

> Perhatian: anda diwajibkan menggunakan *prefix* **file_** pada nama input untuk membantu Puko mengenali inputan tersebut berupa berkas.

Saat ini, Puko baru menyediakan penyimpanan file secara otomatis ke dalam *database* dengan tipe data BLOB.
Untuk menyimpan data anda dapat membuat array untuk menyiapkan semua data dengan ketentuan key pada array harus sama dengan nama kolom di database seperti berikut.

```php
$data = array(
    'nama' => $nama,
    'file_data' => $_FILES['file_berkas']['tmp_name'],
    ...
);
```

> Perhatian: anda juga diwajibkan menggunakan *prefix* **file_** pada nama kolom dengan tipe data BLOB di database.

Atau, jika nama kolom yang telah dibuat tidak mengandung *prefix* **file_** anda dapat menggunakan sintaks file_get_contents() 
seperti yang dicontohkan berikut ini.

```php
$data = array(
    'nama' => $nama,
    'file_data' => file_get_contents($_FILES['file_berkas']['tmp_name']),
    ...
);
```

Jika array data telah siap, anda bisa langsung melakukan input data dengan contoh sintaks berikut.

```php
DBI::Prepare('tabel')->Save($data, true);
```

```php
DBI::Prepare('tabel')->Update($where, $data, true);
```

Parameter *true* digunakan jika anda tidak menggunakan file_get_contents().
Bila menggunakan file_get_contents() anda harus merubahnya menjadi *false*.

> Perhatian: penjelasan penggunaan **DBI** dapat anda lihat secara lengkap pada sesi tutorial **Database**.