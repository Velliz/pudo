---
title: Elements
category: Puko Template Engine
order: 2
---

Element adalah sebuah *feature set* dari puko template engine yang dapat berdiri sendiri, dapat di lepas pasang, serta dipakai ulang.
Element sendiri terdiri dari satu paket file template *html*, *JavaScript* dan kelas PHP untuk mengatur logic dari element tersebut.

Untuk mengunduh set Element, anda bisa menggunakan *command* berikut.
 
```text
php puko element download adminlte_description
```

> Perhatian: anda dapat melihat element apa saja yang tersedia untuk diunduh dari halaman [berikut](https://github.com/Velliz/elements)

Anda juga dapat membuat sebuah elemen baru dengan perintah.

```text
php puko element add ...
```

Anda bisa menamainya bebas sesuai dengan keinginan anda.

> Perhatian: penamaan element tidak boleh menggunakan spasi atau angka di depan.

Setelah sebuah element terbentuk atau didownload, maka element akan tersimpan pada direktori.

```text
- plugins
  - elements
   - ...
     - ....php
     - ....html
     - ....js
     - ....css
```

Untuk percobaan, anda dapat memulainya dari mendownload terlebih dahulu sampel berikut.

```text
php puko element download adminlte_description
```

Lalu membuat instansiasinya dari controller.

```php
public function profile() {
    $desc = new AdminLTE_Description('desc', array());
    $desc->SetStyle(AdminLTE_Description::HORIZONTAL);
    $desc->SetDescription(array(
        array(
            'Title' => 'Didit Velliz',
            'Text' => 'Programmer',
        ),
        array(
            'Title' => 'Lois',
            'Text' => 'Gamer',
        ),
        array(
            'Title' => 'Christian',
            'Text' => 'Lead Developer',
        )
    ));
    $data['desc'] = $desc;
}
```

Pada halaman html, anda dapat merender tag tersebut dengan menuliskan.

```html
<div>{!desc}</div>
```