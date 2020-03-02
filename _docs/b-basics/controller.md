---
title: Controller
category: Basics
order: 2
---

Karena file controller dibuat secara otomatis dengan *Scaffolding* pada saat pembuatan Routes, tentu anda tidak perlu lagi membuat file controller secara manual.
Namun, ada beberapa hal yang perlu diperhatikan mengenai struktur dari file controller yaitu.

* Controller di *Puko* memiliki namespace.

```php
namespace controller;
```

```php
namespace controller\akun;
```

* Controller di *Puko* selalu turunan dari kelas **View** / **Service** / **Console**.

```php
class member extends View {
```

```php
class member extends Service {
```

```php
class member extends Console {
```

* Controller di *Puko* hanya mengirimkan data ke **View** / **Service** melalui fitur *return* dari *function*.

```php
public function member() {
    $data['Nama'] = 'Didit Velliz';
    $data['Alamat'] = 'Bandung';
    return $data;
}
```

* Controller di **Puko** memiliki fitur pelengkap yang bisa anda sisipkan melalui *doc tags*.

```php
/**
 * #Value Hobi Berenang
 * #Auth bearer true
 */
public function member() {
    $data['Nama'] = 'Didit Velliz';
    $data['Alamat'] = 'Bandung';
    return $data;
}
```

> Perhatian: fitur *doc tags* dapat anda lihat secara lengkap pada sesi tutorial **Puko Docs Command**.