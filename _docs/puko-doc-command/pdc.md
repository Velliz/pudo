---
title: Puko Doc Command
category: Puko Doc Command 
order: 1
---

Untuk mempercepat pembangunan aplikasi *Puko* mempunyai *command* yang penerapannya 
dilakukan dengan menulis komentar pada bagian atas *controller* maupun *function* seperti misalnya pada contoh berikut.

```php
/**
 * #Value title Selamat Datang
 * #Master master-admin.html
 * #Date before 31-08-2016 12:00:00
 */
 public class registrasi extends View {
```

Penulisannya mirip seperti sintaks dasar untuk membubuhkan komentar.
Namun, untuk membedakannya dari komentar atau anotasi, maka *command* perlu ditambahkan hashtag.

```php
/**
 * #
 */
```

Berikut ini adalah tabel lengkap daftar *command* yang tersedia.

|*Command*|Key Identifier|Nilai|Fungsi|
|#Value|nama|Didit Velliz|Untuk mengirimkan data bernama **nama** dengan nilai **Didit Velliz** secara langsung ke view|
|#Template|master|true/false|Pilihan untuk menggunakan master layout|
|#Template|html|true/false|Opsi untuk mengeluarkan html file pada browser|
|#Template|cache|true/false|Opsi untuk melakukan cache pada file html|
|#Date|before/after|d-m-Y H:i:s|Opsi untuk pengaksesan **function** Jadi kalau waktu server diluar waktu yang ditentukan maka **function** tidak dapat diakses|
|#ClearOutput|binary|true/false|Opsi untuk mengeluarkan result yang diproses melalui framework|
|#Auth|true/false|+|Opsi untuk pengaksesan fungsi. true untuk mengijinkan yang sudah login saja, false untuk mengijinkan semua|
|#Master|-|master.html|Mengunakan custom file untuk master layout|
|#DisplayException|-|true/false|Meneruskan proses ke *View* / *Service* saat terjadi exception|

> Perhatian: ClearOutput sudah ditinggalkan sejak versi >= 1.1.0
