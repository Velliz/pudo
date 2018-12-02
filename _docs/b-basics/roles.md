---
title: Roles
category: Basics
order: 7
---

Untuk mengimplementasikan role, anda perlu memodifikasi kode login seperti contoh berikut.

```php
public function Login($username, $password)
{
    $siswa = SiswaModel::GetByUsernamePassword($username, md5($password));
    
    Session::Get($this)->SetPermission(array(
        'SISWA', 'ALUMNI'
    ));
    
    return $siswa['ID'];
}
```

**Session::Get($this)->SetPermission()** digunakan untuk menandakan role apa saja yang diperbolehkan oleh user yang sudah login.

Jika role telah ditetapkan, anda dapat menggunakannya dengan mengganti tanda + dengan role yang dimaksudkan.

```php
/**
 * #Auth session true
 */
public function profile() {
```

Ditambahkan menjadi seperti ini jika ingin mengijinkan siswa saja.

```php
/**
 * #Auth session true
 * #Permission \pukoframework\auth\Session@\plugins\auth\UserAuth permissions@SISWA
 */
public function profile() {
```

Dirubah menjadi seperti ini jika ingin mengijinkan alumni saja.

```php
/**
 * #Auth session true
 * #Permission \pukoframework\auth\Session@\plugins\auth\UserAuth permissions@ALUMNI
 */
public function profile() {
```