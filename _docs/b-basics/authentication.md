---
title: Authentication
category: Basics
order: 6
---

*Authentication* pada Puko Framework dapat dibuat lewat *Scaffolding*. 

```text
php puko setup auth ...
```

Dengan parameter ... yang bisa anda isi sesuai dengan nama kelas yang anda inginkan. 
Anda juga bisa membuat beberapa jenis *Authentication* seperti berikut.

```text
php puko setup auth SiswaAuth
```

```text
php puko setup auth DosenAuth
```

```text
php puko setup auth JurusanAuth
```

Sebuah *file class* akan otomatis dibuat sesuai dengan nama yang diisikan. Anda bisa melihatnya pada direktori.

```text
- plugins/
  - auth/
    - SiswaAuth.php
```

Jika *file* tersebut dibuka, maka akan terlihat tiga fungsi ini menunggu untuk dilengkapi.

```php
public function Login($username, $password)
{
    //todo: your custom login code here
}

public function Logout()
{
    //todo: create or clear log in databases
}

public function GetLoginData($id)
{
    //todo: return your user data here
}
```

**Login($username, $password)**

Untuk implementasi login, anda bisa menuliskan logika login dalam fungsi ini.
Misalnya melakukan *select* data dari database seperti contoh berikut.

```php
public function Login($username, $password)
{
    $siswa = SiswaModel::GetByUsernamePassword($username, md5($password));
    return $siswa['ID'];
}
```

> Perhatian: Login wajib melakukan return ID atau *single value* lain sebagai patokan data yang akan disimpan oleh framework ke dalam COOKIES. 

Kemudian, anda dapat menjalankan *function* Login pada controller seperti contoh berikut.

```php
$login = Session::Get(SiswaAuth::Instance())->Login($username, $password, Auth::EXPIRED_1_WEEK);
```

**SiswaAuth::Instance()** merupakan pemagilan objek dari kelas yang telah kita modifikasi kode loginnya.
 
**Auth::EXPIRED_1_WEEK** Adalah *static value* yang dapat digunakan untuk menentukan lamanya login.
Terdapat beberapa *static value* lain yaitu.

|EXPIRED_1_HOUR|
|EXPIRED_1_DAY|
|EXPIRED_1_WEEK|
|EXPIRED_1_MONTH|

Jika login berhasil, maka variabel **$login** akan bernilai *true*. Jika gagal variabel **$login** akan bernilai *false*.

**Logout()**

Anda bisa menuliskan kode apa yang akan dijalankan sebelum user melakukan logout.
Misalnya membuat log dan sebagainya dengan contoh sebagai berikut.
                                           
```php
public function Logout()
{
    $date = new DateTime();
    SiswaModel::LogoutStamps($date->format('Y-m-d H:i:s'));
}
```

**GetLoginData($id)**

Untuk mengambil kembali data yang telah di *return* dari fungsi login kamu bisa menggunakan *function* ini.
parameter masukan *$id* adalah nilai yang di *return* dari fungsi Login.

Pada contoh di atas kita menyimpan ID dari user siswa yang berhasil login. 
Sehingga untuk mendapatkan data user siswa yang lengkap, maka kita bisa melakukan panggilan *model* seperti contoh berikut.
 
```php
public function GetLoginData($id)
{
    return SiswaModel::GetUserById($id);
}
```

Jika login telah berhasil, anda dapat melindungi *function* yang ada dengan *command* berikut.
```php
/**
 * #Auth session true
 */
```