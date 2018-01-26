---
title: View
category: Basics
order: 4
---


Melanjutkan dokumentasi dari controller dasar. Kali ini mari kita bahas tentang controller yang menjadi View.
Singkatnya, jika kamu mempunyai.

```php
namespace controller;

use pukoframework\pte\View;

class yourclass extends View {
    
    public function yourmethod(){}
    ...
}
```

maka kamu wajib menyertakan file .html sebagai pendamping controller kamu.

```
- assets/
  - html/
    - id/
      - yourclass/
        - master.html
        - yourmethod.html
```

Jadi, setiap kelas **yourclass** kamu wajib memiliki sebuah file bernama **master.html** sebagai induk layout.
Jadi kamu TIDAK BOLEH membuat function atau nama method dengan nama **master**. 
Berikut contoh dari file master.html

```
<!DOCTYPE html>
<html>
<head>
    <title>{!PageTitle}</title>
</head>
<body>
    {CONTENT}
</body>
```

dimana nantinya yourmethod.html akan berada pada **{CONTENT}**.
Kemudian kita juga memiliki tag bernama {!PageTitle}. 
Kita bisa mengisi nilai dari {!PageTitle} tersebut dengan menambahkan **return** data berjenis **array()**
pada method atau function seperti

```php
public function yourmethod()
{
    return array('PageTitle' => 'Puko Framework');
}   
```

nah, jika kamu membuka halaman web-nya sekarang maka {!PageTitle} sudah memiliki nilai **Puko Framework** 
Intinya, jika kamu ingin mengirim data untuk halaman .html kamu perlu melakukan **return** data bertipe array pada akhir function kamu.
Untuk lebih jelasnya mengenai template dan data silahkan membaca bagian dokumentasi Puko Template Engine (PTE).