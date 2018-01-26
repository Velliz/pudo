---
title: Authentication
category: Basics
order: 7
---

Login, Logout dan Session pada Puko Framework dapat diatur dari controller. cara menggunakannya adalah dengan mengimplementasikan interface bernama **Auth**.
Jika kamu mengimplementasikan interface ini, otomatis wajib mengimplementasikan / override tiga buah method bernama 

* public function Login($username, $password)
* public function Logout()
* public function GetLoginData($id)

contohnya seperti ini:

```php
namespace controller;

use pukoframework\auth\Auth;
use pukoframework\auth\Session;
use pukoframework\pda\DBI;
use pukoframework\pte\View;
use pukoframework\Request;

class member extends View implements Auth
{
    #region auth
    public function Login($username, $password)
    {
        
    }

    public function Logout()
    {

    }

    public function GetLoginData($id)
    {
        
    }
    #end region auth
}
```

#### **Login**

Untuk keperluan login, kamu bisa menuliskan logika login dalam fungsi **Login($username, $password)**
Misalnya select data dari database. contohnya seperti ini

```php
public function Login($username, $password)
{
    $loginResult = Database::GetUser($username, md5($password))[0];
    // return data yang akan disimpan di session selama login
    return $loginResult['ID'];
}
```

kemudian menjalankan function Login kamu melalui function lain misal pada 'main'

```php
Session::Get($this)->Login($username, md5($password), Auth::EXPIRED_1_WEEK)
```

untuk parameter ketiga yaitu **Auth** terdapat beberapa pilihan untuk menentukan lamanya login yaitu:

|EXPIRED_ON_CLOSE|
|EXPIRED_1_HOUR|
|EXPIRED_1_DAY|
|EXPIRED_1_WEEK|
|EXPIRED_1_MONTH|

Contoh

```php
public function main()
{
    if (Request::IsPost()) {
        $username = Request::Post('username', null);
        if ($username == null) throw new \Exception('PIC/Username must filled');
        $password = Request::Post('password', null);
        if ($password == null) throw new \Exception('Password must filled');
        if (Session::Get($this)->Login($username, md5($password), Auth::EXPIRED_1_MONTH)) {
            //login berhasil
            return;
        }
        throw new \Exception('Username or password not exists.');
    }
}
```

Jika login berhasil, Puko Framework akan membuat sebuah COOKIE bernama puko.

#### **Logout**

Sedangkan untuk logout, kamu bisa menuliskan juga kode apa yang akan dijalankan sebelum user tersebut logout.
Misalnya menghapus cookies dan sebagainya. contohnya seperti ini
                                           
```php
public function Logout()
{
   unset($_COOKIE['cart']);
}
```

#### **Get Login Data**

Untuk mengambil data yang telah di return dari fungsi login kamu bisa menggunakan public **function GetLoginData($id)**
dimana $id adalah parameter berisi data yang di-return pada fungsi Login.
Pada contoh diatas kita hanya menyimpan ID dari user yang berhasil login. 
Sehingga untuk mendapatkan data user lain selain ID maka kita harus menambahkan kodenya.
 
```php
public function GetLoginData($id)
{
    return DBAnywhere::GetUserById($id)[0];
}
```

#### **Session**

Sessions pada puko terbuat secara otomatis ketika function Login mengembalikan data yang juga tersimpan sebagai session value.
Pada cookie browser dapat dilihat dengan nama puko dan nilainya terenkripsi.
Disarankan untuk tidak menyimpan data kurang dari 16 kb kedalam session karena kapasitas cookie yang terbatas.
