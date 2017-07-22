---
layout: page
title: "Puko Template Engine"
category: doc
date: 2017-07-22 14:32:49
order: 21
---



Puko Template Engine adalah agen yang ditugas khususkan untuk mengolah tampilan. Untuk penggunaanya, Intinya kamu harus punya kelas controller yang bertipe View.
Kemudian kamu juga harus memiliki return data array pada setiap functionnya. Untuk memudahkan, kamu bisa membuat contoh controller seperti berikut.

```
namespace controller;
use pukoframework\pte\View;

class main extends View implements Auth
{

    public function main()
    {
        $hello = array();
        $hello['PageTitle'] = 'Latihan Pertama';
        $hello['SomeKey'] = 'Agustus';
        $hello['Description'] = 'Deskripsi Pembangunan dengan PTE';
        $hello['Member'] = array(
            array(
                'ID' => '1',
                'Nama' => 'Velliz',
                'Usia' => 12
            ),
            array(
                'ID' => '2',
                'Nama' => 'Didit',
                'Usia' => 18
            ),
            array(
                'ID' => '3',
                'Nama' => 'Puko',
                'Usia' => 11
            )
        );
        $hello['Block'] = false;
        return $hello;
    }
    
}
```

Lalu, buatlah dua buah file .html pada direktori

```
- assets/
  - html/
    - id/
      - main/
        - master.html
        - main.html
```

master.html berfungsi sebagai indukan file, jadi kamu tidak perlu repot untuk menulis <head> dan <footer> berulang ulang disetiap page.
untuk detilnya kamu bisa melihat contoh berikut.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{!PageTitle}</title>
</head>
<body>
{CONTENT}
</body>
</html>
```

{CONTENT} adalah tag yang khusus terdapat di master.html. 
Fungsinya adalah sebagai penanda view yang dihasilkan oleh function kamu. 
Jadi, jika kamu mengeksekusi function main, maka {CONTENT} akan berubah menjadi hasil dari main.html dan seterusnya.

Sekarang kita coba isi file main.html dengan contoh berikut.

```
<h3>{!SomeKey}</h3>
<p>{!Description}</p>

<table border="1">
    <tr>
        <th>ID</th>
        <th>Nama</th>
        <th>Usia</th>
    </tr>
    <!--{!Member}-->
    <tr>
        <td>{!ID}</td>
        <td>{!Nama}</td>
        <td>{!Usia}</td>
    </tr>
    <!--{/Member}-->
</table>

<!--{!!Block}-->
<span>Terimakasih</span>
<!--{/Block}-->
```

Jika kamu membuka halaman websitenya sekarang, kamu akan menemukan bahwa browser menerima file seperti ini.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Latihan Pertama</title>
</head>
<body>
<h3>Agustus</h3>
<p>Deskripsi Pembangunan dengan PTE</p>

<table border="1">
    <tr>
        <th>ID</th>
        <th>Nama</th>
        <th>Usia</th>
    </tr>
    
    <tr>
        <td>1</td>
        <td>Velliz</td>
        <td>12</td>
    </tr>
    
    <tr>
        <td>2</td>
        <td>Didit</td>
        <td>18</td>
    </tr>
    
    <tr>
        <td>3</td>
        <td>Puko</td>
        <td>11</td>
    </tr>
    
</table>

<span>Terimakasih</span>

</body>
</html>
```

Artinya Template kamu sudah berhasil dirender oleh PTE. 

Berikut tabel yang menjelaskan tentang tag yang tersedia pada PTE.

|Tipe PTE|Key PTE|Contoh Data Controller|Keterangan|
|Value|{!Value}|return array('Value' => 'Hello World')|Simple Value Render|
|Blocked Condition|&lt;!--{!!Block}--&gt;&lt;!--{/Block}--&gt;|return array('Block' => false)|Output or Hide View Segments|
|Loop|&lt;!--{!Member}--&gt;&lt;!--{/Member}--&gt;|return DBI::Prepare('Member')->GetData();|Looping Output from Database GetData()|

#### **Assets**

Ketika menggunakan sistem master layout, 
ada saat dimana kita menginginkan sebuah file script/javascript dan style/css tertentu untuk diload pada halaman tertentu saja.
cara sederhanannya adalah dengan menuliskannya pada template kamu dengan cara:
 
```
{!CSS}
<link href="{URL}assets/global/plugins/bootstrap/css/bootstrap.min.css" rel="stylesheet" type="text/css" />
{/CSS}

<h3>{!SomeKey}</h3>
<p>{!Description}</p>

<table border="1">
    <tr>
        <th>ID</th>
        <th>Nama</th>
        <th>Usia</th>
    </tr>
    <!--{!Member}-->
    <tr>
        <td>{!ID}</td>
        <td>{!Nama}</td>
        <td>{!Usia}</td>
    </tr>
    <!--{/Member}-->
</table>

<!--{!!Block}-->
<span>Terimakasih</span>
<!--{/Block}-->

{!JS}
<script src="{URL}assets/global/plugins/jquery.min.js" type="text/javascript"></script>
{/JS}
```

Kemudian kamu tinggal mendefinisikan dimaster layout, penempatan mereka seperti:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{!PageTitle}</title>
    {CSS}
</head>
<body>
{CONTENT}
</body>
{JS}
</html>
```

Maka secara otomatis puko akan memindahkan posisi script/javascript dan style/css ke master layout.

**TODO: PTE Lainnya**