---
title: Error, Exception and Not Found
category: Basics
order: 9
---

Untuk menangani kesalahan. Sebuah website perlu menampilkan pesan yang manusiawi bagi user. 
Misalkan error karena kesalahan pengetikan URL. Error karena user terlebih dahulu harus login dan semacamnya, 
anda bisa mengatur tiga kategori halaman yaitu.

**Error**

Halaman ini dibuka katika *http verb* yang dijinkan tidak sesuai. Anda bisa membuatnya dengan *command* berikut.

```text
php puko routes error add ...
```

**Not Found**

Halaman ini dibuka ketika halaman tidak ditemukan pada daftar routing. Anda bisa membuatnya dengan *command* berikut.

```text
php puko routes not_found add ...
```

---

Selain itu, anda juga dapat mengatur beberapa halaman error dari sistem internal *Puko* diantaranya.

**Exception**

Halaman ini dibuka ketika sebuah Exception terjadi. Anda tidak bisa membuat halamannya karena diatur oleh *Puko* secara internal.
Namun, anda bisa mengaplikasikan css atau mengubah struktur halamannya melalui *file* berikut.

```text
- assets/
  - systems/
    - exception.html
```

**Not Authenticated**

Halaman ini dibuka ketika user yang tidak login mencoba membuka halaman yang dilindungi. Anda tidak bisa membuat halamannya karena diatur oleh *Puko* secara internal.
Namun, anda bisa mengaplikasikan css atau mengubah struktur halamannya melalui *file* berikut.

```text
- assets/
  - systems/
    - auth.html
```

**Not Authorized**

Halaman ini dibuka ketika user yang login tidak memiliki cukup role. Anda tidak bisa membuat halamannya karena diatur oleh *Puko* secara internal.
Namun, anda bisa mengaplikasikan css atau mengubah struktur halamannya melalui *file* berikut.

```text
- assets/
  - systems/
    - permission.html
```
