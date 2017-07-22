---
layout: page
title: "Controller"
category: doc
date: 2017-01-01 14:31:44
order: 1
---


Seperti kebanyakan MVC Framework lainnya, Puko Framework memiliki controller yang lokasinya berada didalam folder controller.
Kamu bisa membuat file controller ini dengan aturan penamaan **file** dan nama kelas sesuai dengan nama **file**. 
Serta nama **function** dengan menggunakan huruf kecil semua.

controller pada Puko Framework juga wajib diberi namespace

```PHP
namespace controller;
```

sebagai pertanda bahwa kelas tersebut masuk kedalam paket controller.
Selain itu yang tidak kalah penting adalah kamu harus mendefinisikan controller tersebut apakah controller tersebut berperilaku sebagai
**View** atau **Service**. 

**View** adalah tipe controller yang pada final prosessnya akan meload file .html yang memiliki nama sama dengan nama controller tersebut.
Sedangan **Service** adalah tipe controller yang pada final prosessnya akan mengeluarkan data dalam bentuk JSON.

Contoh menggunakan **View**

```PHP
<?php
namespace controller;

use pukoframework\pte\View;

class member extends View
{   
    function main()
    {
    }
}
```

Contoh menggunakan **Service**

```PHP
<?php
namespace controller;

use pukoframework\pte\Service;

class member extends Service
{   
    function main()
    {
    }
}
```

Secara default, nama kelas menjadi segmen 1 dalam URL website.
dan nama *function* di controller kamu menjadi segmen 2 dalam URL website.
Segmen selanjutnya akan menjadi parameter masukan untuk *function*.

Contoh:

|Nama Controller|Nama Function|URL|
|class member|public function main|example.com/?request=member/main|
|class member|public function register|example.com/?request=member/register|
|class admin|public function views|example.com/?request=admin/views|
|class admin|public function views($id){}|example.com/?request=admin/views/1|
|class admin|public function views($id, $username, $age){}|example.com/?request=admin/views/1/velliz/22|

