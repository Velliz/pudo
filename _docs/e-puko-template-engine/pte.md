---
title: Puko Template Engine
category: Puko Template Engine
order: 1
---

Puko Template Engine is a package that helps *Puko* process displayed html.
All tags that can be used are summarized in the following table.

|Tags|Description|
|---|---|
| {!x} | tags to print values, data or elements |
| `<!--{!x}-->` | **open** looping tag |
| `<!--{/x}-->` | **close** looping tag |
| {!fn()} | **function** tag without parameter |
| {!fn(x)} | **function** tag with one parameter |
| {!fn(x,y,z)} | **function** tag with many parameters |
| {CONTENT} | **CONTENT** tag for injecting content html file to master *file* |
| {!css(<link href="" rel="stylesheet" type="text/css" />)} | **CSS** tag |
| {!js(<script src="" type="text/javascript"></script>)} | **JavaScript** tag |
| {!part(css)} | move **CSS** tag from content html to tag location somewhere in master |
| {!part(js)} | move **JavaScript** tag from content html to tag location somewhere in master |
| {x.html} | tag for load segment file |

> Attention: **Elements** can be seen in the **Elements** document section.

```html
<span>{!x}</span>
```

The value `x` can be exchanged into other values by means of.

```php
public function siswa() {
    $data['x'] = 34;
    return $data;
}
```

The result, will look like the following:

```html
<span>34</span>
```

You can also convert `x` into other variables as needed.

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

The value **student** which is a looping tag can be echoed as list of data in pte view rendering process.

```php
public function siswa() {
    $data['siswa'] = Siswa::GetAll();
    return $data;
}
```

Or, directly hardcode the data for now as projection.

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

The result, will look like the following:

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

---

You can write the use of assets on content like the following example.

```html
{!css(<link href="assets/css/bootstrap.min.css" rel="stylesheet" type="text/css"/>)}

{!js(<script src="assets/js/jquery.dataTables.min.js"></script>)}
{!js(<script src="assets/js/dataTables.bootstrap.min.js"></script>)}
```

Make sure you also have forwarded the file to the master template.
Usually, in the master template there by default will have the following input tags.

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

---

To get website `base url` in html file, write the following function syntax:

```text
{!url()}
```

```text
{!url()}user/beranda
```