---
title: Puko Template Engine
category: Puko Template Engine
order: 1
---

Puko Template Engine adalah package yang membantu *Puko* mengolah tampilan. 
Semua tag yang bisa digunakan terangkum pada tabel berikut.

| Tags | Description |
| --- | --- |
| {!x} | tag untuk mencetak nilai atau **Elements** |
| `<!--{!x}-->` | **open** looping tag |
| `<!--{/x}-->` | **close** looping tag |
| {!fn()} | **function** tag tanpa parameter |
| {!fn(x)} | **function** tag dengan satu parameter |
| {!fn(x,y,z)} | **function** tag dengan banyak parameters |
| {CONTENT} | **CONTENT** tag hanya dikenali dalam master *file* |
| {!css(<link href="" rel="stylesheet" type="text/css" />)} | **CSS** tag |
| {!js(<script src="" type="text/javascript"></script>)} | **JavaScript** tag |
| {!part(css)} | memindahkan **CSS** tag ke lokasi ini |
| {!part(js)} | memindahkan **JavaScript** tag ke lokasi ini |
| {x.html} | tag untuk segment file |

> Perhatian: **Elements** dapat anda lihat secara lengkap pada sesi tutorial **Elements**.

```html
<span>{!x}</span>
```

Nilai **x** dapat ditukar menjadi nilai lain dengan cara.

```php
public function siswa() {
    $data['x'] = 34;
    return $data;
}
```

Hasilnya, akan tampak menjadi seperti berikut.

```html
<span>34</span>
```

Anda juga dapat mengubah x menjadi variabel lain sesuai kebutuhan.

```html
<table>
    <!--{!siswa}-->
    <tr>
        <td>{!nama}</td>
        <td>{!alamat}</td>
        <td>{!umur}</td>
    </tr>
    <!--{/siswa}-->
</table>
```

Nilai **siswa** yang merupakan tag perulangan dapat ditukar menjadi nilai lain dengan cara.

```php
public function siswa() {
    $data['siswa'] = Siswa::GetAll();
    return $data;
}
```

```php
public function siswa() {
    $data['siswa'] = array(
        array(
            'nama' => 'Didit Velliz',
            'alamat' => 'Bandung',
            'umur' => 12
        ),
        array(
            'nama' => 'Puko Framework',
            'alamat' => 'Jakarta',
            'umur' => 18
        )
    );
    return $data;
}
```

Hasilnya, akan tampak menjadi seperti berikut.

```html
<table>
    <tr>
        <td>Didit Velliz</td>
        <td>Bandung</td>
        <td>12</td>
    </tr>
    <tr>
        <td>Puko Framework</td>
        <td>Jakarta</td>
        <td>18</td>
    </tr>
</table>
```

Penggunaan assets pada content dapat anda tuliskan seperti contoh berikut ini.

```html
{!css(<link href="assets/css/bootstrap.min.css" rel="stylesheet" type="text/css"/>)}

{!js(<script src="assets/js/jquery.dataTables.min.js"></script>)}
{!js(<script src="assets/js/dataTables.bootstrap.min.js"></script>)}
```

Pastikan anda juga telah melakukan forwarding file tersebut ke master template.
Biasanya, di master template akan ada tag input berikut.

```html
<html>
    <head>...</head>
    <body>
    ...
    {CONTENT}
    ...
    {!part(css)}
    {!part(js)}
    </body>
</html>
```

Untuk mendapatkan *base url*, dapat menuliskan sintaks fungsi berikut.

```text
{!url()}
```

```text
{!url(user/beranda)}
```