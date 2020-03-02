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

> pemisahan direktori controller dilakukan dengan memberikan tanda (\) _backslash_

```text
function       : ...
```

```text
accept         : ...
```

> pemisahan beberapa _HTTP verb_ dilakukan dengan memberikan tanda (,) koma

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

> Perhatian: anda diwajibkan menggunakan (\) _backslash_ untuk penamaan di rektori controller.

Karena console telah membuatkan semua halaman yang dibutuhkan termasuk file html-nya. 
Anda dapat langsung membuka halaman yang anda buat dan melihat hasil halaman kosong berhasil di tampilkan.

Anda juga dapat membuat Routing untuk api dengan perintah.

```text
php puko routes service add ...
```

Serta sebuah perintah console yang dapat dieksekusi lewat cli.

```text
php puko routes console add ...
```

> karena console dijalankan tanpa web server, maka _HTTP verb_ yang valid adalah default: GET

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
$routes = [
    "router" => [],
    "error" => [
        "controller" => "error",
        "function" => "display",
        "accept" => [
            "GET",
            "POST"
        ]
    ],
    "not_found" => [
        "controller" => "error",
        "function" => "notfound",
        "accept" => [
            "GET",
            "POST"
        ]
    ],
    "maintenance" => [
        "controller" => "error",
        "function" => "maintenance",
        "accept" => [
            "GET",
            "POST"
        ]
    ]
];
return $routes;
```