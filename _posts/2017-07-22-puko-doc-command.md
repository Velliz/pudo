---
layout: page
title: "Puko Doc Command"
category: doc
date: 2017-07-22 14:32:39
order: 7
---

Untuk mempercepat pembangunan aplikasi, Puko Framework mempunyai utilitas PDC yang penerapannya dilakukan dengan menulis komentar pada file **controller**
Yup, komentar seperti misalnya:

```
/**
 * #Value nama Didit Velliz
 * #Template master false
 * #Template html false
 * #Date before 31-08-2016 12:00:00
 * #Date after 10-09-2016 12:00:00
 */
 public function registrasi {
```

Dengan syntax dasar komentar pada umumnya sebagai berikut.

```
/**
 * #
 */
```

|Command|Key Identifier|Nilai|Fungsi|
|#Value|nama|Didit Velliz|Untuk mengirimkan data bernama **nama** dengan nilai **Didit Velliz** secara langsung ke view|
|#Template|master|true/false|Pilihan untuk menggunakan **master.html** layout|
|#Template|html|true/false|Opsi untuk mengeluarkan html file pada browser|
|#Date|before/after|d-m-Y H:i:s|Opsi untuk pengaksesan **function** Jadi kalau waktu server diluar waktu yang ditentukan maka **function** tidak dapat diakses|
|#ClearOutput||true/false|Opsi untuk membersihkan semua tag '{!}' kosong. true untuk membersihkan, false untuk tetap menampilkannya.|
|#Auth||true/false|Opsi untuk pengaksesan fungsi. true untuk mengijinkan yang sudah login saja, false untuk mengijinkan semua.|

**TODO: PDC Lainnya**

Selain itu PDC juga dapat diterapkan diatas nama kelas. Artinya PDC akan diberlakukan di semua **function** yang ada didalam kelas tersebut. 
Tetapi jika kemudian PDC didefinisikan lagi di **function** maka PDC yang digunakan adalah yang didefinisikan di **function**.

Contoh sederhananya sebagai berikut.

```
/**
 * #Value nama Didit Velliz
 */
 public class member {
    
    /**
     * #Value nama Puko Framework
     */
    public function registrasi()
    {
    }
    
    public function thankyou()
    {
    }
 }
```

yang artinya jika kamu memanggil **registrasi** berarti nama adalah Puko Framework.
Jika kamu memanggil **thankyou** berarti nama adalah Didit Velliz. Yup! gampang kan!
