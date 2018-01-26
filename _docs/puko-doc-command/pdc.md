---
title: Puko Doc Command
category: Puko Doc Command 
order: 1
---

Untuk mempercepat pembangunan aplikasi *Puko Framework* mempunyai utilitas yang penerapannya 
dilakukan dengan menulis komentar pada file **controller** komentar seperti misalnya pada kelas

```php
namespace controller;

/**
 * #Value nama Didit Velliz
 * #Template html false
 * #Date before 31-08-2016 12:00:00
 */
 public class registrasi extends View {
```

Dengan syntax dasar komentar yang pada umumnya sebagai berikut. 
Namun untuk menandai komentar adalah command maka perlu ditambahkan hashtag #

```php
/**
 * #
 */
```

Berikut ini adalah tabel lengkap daftar command yang tersedia.

|Command|Key Identifier|Nilai|Fungsi|
|#Value|nama|Didit Velliz|Untuk mengirimkan data bernama **nama** dengan nilai **Didit Velliz** secara langsung ke view|
|#Template|master|true/false|Pilihan untuk menggunakan **master.html** layout|
|#Template|html|true/false|Opsi untuk mengeluarkan html file pada browser|
|#Date|before/after|d-m-Y H:i:s|Opsi untuk pengaksesan **function** Jadi kalau waktu server diluar waktu yang ditentukan maka **function** tidak dapat diakses|
|#ClearOutput|-|true/false|Opsi untuk membersihkan semua tag '{!}' kosong. true untuk membersihkan, false untuk tetap menampilkannya|
|#Auth|true/false|+|Opsi untuk pengaksesan fungsi. true untuk mengijinkan yang sudah login saja, false untuk mengijinkan semua|
|#Master|-|master.html|Mengunakan custom file untuk master layout|

Selain itu PDC juga dapat diterapkan diatas nama controller. 
Jika PDC didefinisikan di **function** dan **class** maka PDC yang digunakan adalah yang didefinisikan di **function**.

Contoh sederhananya sebagai berikut.

```php
namespace controller;

/**
 * #Value nama Didit Velliz
 */
 public class member extends View {
    
    /**
     * #Value nama Puko Framework
     */
    public function registrasi()
    {
    }
    
    /**
    * #Auth true +
    */
    public function thankyou()
    {
    }
 }
```

Artinya jika kamu memanggil **registrasi** berarti nama adalah Puko Framework.
Jika kamu memanggil **thankyou** berarti nama adalah Didit Velliz.
