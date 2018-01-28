---
title: Routing
category: Basics
order: 1
---

Routing pada *Puko* dilakukan secara otomatis dengan fitur bernama *Scaffolding* melalui aplikasi console / *command prompt*.
Untuk menambahkan sebuah halaman baru dengan *output* berupa halaman html yang ditampilkan melalui browser anda dapat memasukan perintah.

```text
php puko routes view add ...
```

pada bagian ... anda dapat mendefinisikan alamat halaman anda dengan aturan REST.
Anda juga bisa menambahkan parameter sebagai segmen dengan tanda {?}.
Berikut ini merupakan beberapa contoh alamat yang valid.

```text
php puko routes view add profile
```

```text
php puko routes view add member/{?}
```

```text
php puko routes view add akun/tautan
```

```text
php puko routes view add akun/gudang/barang
```

```text
php puko routes view add akun/{?}/barang
```

```text
php puko routes view add dashboard/user/{?}/kurtal/{?}
```

Untuk melanjutkan, anda bisa menekan tombol enter. Kemudian console akan meminta informasi tambahan berupa lokasi
*controller*, *function* dan *HTTP verb* dari *routing* yang anda buat.

```text
controller     : ...
```

```text
function       : ...
```

```text
accept         : ...
```

Anda dapat menuliskan dimana letak file. Contoh penulisan yang dianggap valid adalah sebagai berikut.

```text
controller     : user
function       : profile
accept         : GET
```

Opsi ini akan memerintahkan console membuat file controller user.php dan function profile secara otomatis.

```text
controller     : akun\user
function       : profile
accept         : GET,POST
```

Opsi ini akan memerintahkan console membuat file controller user.php di dalam folder akun dan function profile secara otomatis.

```text
controller     : akun\gudang\user
function       : profile
accept         : GET,POST,PUT,HEAD
```

Opsi ini akan memerintahkan console membuat file controller user.php di dalam folder gudang yang berada didalam folder akun dan function profile secara otomatis.

> Perhatian: anda diwajibkan menggunakan backslash \ untuk penamaan di rektori controller.

Karena console telah membuatkan semua halaman yang dibutuhkan termasuk file html-nya. 
Anda dapat langsung membuka halaman yang anda buat dan melihat hasil halaman kosong berhasil di tampilkan.

Perlu diperhatikan juga bahwa anda dapat membuat Routing untuk api dengan perintah.

```text
php puko routes service add ...
```

Serta perubahan pada Routing yang anda buat dengan sintaks *update* atau *delete* dengan perintah.

```text
php puko routes service update ...
```

```text
php puko routes service delete ...
```

Anda juga dapat melihat seluruh Routes yang telah terdaftar dengan perintah.

```text
php puko routes view list
```

Anda juga dapat melihat semua konfigurasi yang telah dibuat oleh console tersimpan di dalam file routes.php yang berada dalam folder *config*

```php
$data['page'] = array(
    'profile' => array(
            'controller' => 'akun\\user',
            'function' => 'profile',
            'accept' => ['GET', 'POST'],
    )
);
$data['error'] = array(
    'controller' => 'main',
    'function' => 'error',
    'accept' => ['GET', 'POST', 'PUT', 'HEAD']
);
$data['not_found'] = array(
    'controller' => 'main',
    'function' => 'not_found',
    'accept' => ['GET', 'POST', 'PUT', 'HEAD']
);
return $data;
```