---
layout: page
title: "Permissions"
category: doc
date: 2017-08-28 21:20:53
---

Untuk mengimplementasikan permission pertama lakukan login.

```php
<?php
Session::Get($this)->Login('didit', 'didit', Auth::EXPIRED_1_DAY);
```

Kemudian set permission pada proses login.
```php
<?php
public function Login($username, $password)
{
    Session::Get($this)->SetPermission(array('ADMIN', 'USER'));
    return true;
}
```

Setelah itu bungkus function yang dilindungi dengan PDC.
```php
<?php
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
<?php
/**
 * #Value title HELLO
 * #Auth true +
 */
public function profile()
{
}
```