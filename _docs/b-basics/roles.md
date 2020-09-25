---
title: Roles
category: Basics
order: 7
---

Role is part-of the Auth. You can see it in `PukoAuth` class instance as seconds parameter:

```php
public function Login($username, $password)
{
    ...
    $permission = [];
    return new PukoAuth([], $permission);
}
```

```php
/**
 * #Auth session true
 */
public function profile()
```

Ditambahkan menjadi seperti ini jika ingin mengijinkan siswa saja.

```php
/**
 * #Auth session true
 * #Permission \pukoframework\auth\Session@\plugins\auth\UserAuth permissions@SISWA
 */
public function profile()
```

Dirubah menjadi seperti ini jika ingin mengijinkan alumni saja.

```php
/**
 * #Auth session true
 * #Permission \pukoframework\auth\Session@\plugins\auth\UserAuth permissions@ALUMNI
 */
public function profile()
```