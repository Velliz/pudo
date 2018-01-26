---
title: Service
category: basics
order: 5
---

Kali ini mari kita bahas tentang controller yang menjadi Service.
Singkatnya, jika kamu mempunyai.

```php
<?php

namespace controller;

use pukoframework\pte\Service;

class yourclass extends Service {
    
    public function yourmethod(){}
    ...
}
```

nah, jika kamu membuka halaman web-nya sekarang maka kamu akan mendapatkan output file .json seperti ini.

```json
{
  "time": 0.0010089874267578,
  "status": "success",
  "data": {
    "token": "356cb1c5693c6481e08599b553e50c25b43aca30fbed5ad877a319f6eb7d7a42"
  }
}
```

Perlu diketahui bahwa service akan selalu mengembalikan data bernama *time* dan *token*.
*Time* mengukur seberapa lama data diolah oleh server.
*Token* dapat digunakan untuk mengidentifikasi user yang mengakses Service.
Untuk memunculkan data selain *token*, tambahkan data dengan menggunakan return pada akhir function. 
Contoh.

```php
public function yourmethod()
{
    return array(
        'NIK' => '1266409',
        'Nama' => 'Didit Velliz',
        'Usia' => 22,
        'Keahlian' => array(
            'PHP', 'MySQL'
        )
    );
}
```

Maka pada bagian data array akan muncul bersama dengan *token*.

```json
{
  "time": 0.33715486526489,
  "status": "success",
  "data": {
    "NIK": "1266409",
    "Nama": "Didit Velliz",
    "Usia": 22,
    "Keahlian": [
      "PHP",
      "MySQL"
    ],
    "token": "356cb1c5693c6481e08599b553e50c25b43aca30fbed5ad877a319f6eb7d7a42"
  }
}
```

Selamat! kamu sudah bisa menggunakan output data tersebut untuk keperluan AJAX, Web Service sdb.