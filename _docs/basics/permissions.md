---
title: Permissions
category: Basics
order: 7
---

> Bahaya: fitur ini belum sepenuhnya direkomendasikan untuk implementasi di website untuk production

Untuk mengimplementasikan permission pertama lakukan login.

```php
Session::Get($this)->Login('didit', 'didit', Auth::EXPIRED_1_DAY);
```

Kemudian set permission pada proses login.
```php
public function Login($username, $password)
{
    Session::Get($this)->SetPermission(array('ADMIN', 'USER'));
    return true;
}
```

Setelah itu bungkus function yang dilindungi dengan PDC.
```php
/**
 * #Value title HELLO
 * #Auth true ADMIN USER
 */
public function profile()
{
}
```

Jika hanya menggunakan authentikasi tanpa permission maka bisa ditulis seperti ini.
```php
/**
 * #Value title HELLO
 * #Auth true +
 */
public function profile()
{
}
```