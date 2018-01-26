---
title: Form Validation
category: basics
order: 9
---

Langkah-langkah untuk Validasi form POST cukup mudah.
Pertama yang harus kamu lakukan adalah membuat form dengan ketentuan.

* harus memiliki input type hidden bernama token ber value **{!token}**
* harus memiliki input atau button type submit bernama **_submit**

berikut ini contoh sebuah login form:

```html
<div>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="hidden" name="token" value="{!token}">
        <input type="text" name="username">
        <input type="password" name="password">
        ...
        <input type="submit" name="_submit" value="Login">
    </form>
</div>
```

*action="" mengindikasikan bahwa pengiriman dilakukan ke method itu sendiri.*

untuk melakukan Validasi inputan dengan puko maka kita akan melakukan pengecekan di controller
caranya adalah dengan menangkap POST input yang dikirimkan dengan **Request::Post('name', 'default')**

* *name adalah form name*
* *default adalah nilai pengganti jika tidak diteukan nilai / null*

```
$username = Request::Post('username', null);
$password = Request::Post('password', null);
```

Serta menggunakan **Request::IsPost()** untuk memastikan ke-valid-an form input dan pencegahan dari serangan CSRF (Cross Site Request Forgery)

```
public function login()
{
    if (Request::IsPost()) {
        $username = Request::Post('username', null);
        $password = Request::Post('password', null);

        if ($username == null) throw new Exception("Username harus diisi");
        if ($password == null) throw new Exception("Password harus diisi");

        //logika proses disini
        ...
        //redirect di akhir proses bila perlu 
        $this->RedirectTo('login');
    }
    
    //logika jika tidak ada post data disini
}

```

jadi singkatnya ketika kita menemukan ketidak sesuaian, kita memanggil **throw new Exception("Username harus diisi")**
yang artinya eksekusi controller akan berhenti dan pesan **Username harus diisi** akan dilempar.
untuk menampilkannya kamu cukup menambahkan tag Exception pada file .html kamu.


```
<!--{!!Exception}-->
    {!ExceptionMessage}
<!--{/Exception}-->
```

Kamu dapat menyisipkannya pada awal atau akhir form.

```html
<div>
    <form action="" method="POST" enctype="multipart/form-data">
        <!--{!!Exception}-->
        <div class="alert alert-danger">
            <span>{!ExceptionMessage}</span>
        </div>
        <!--{/Exception}-->
        <input type="hidden" name="token" value="{!token}">
        <input type="text" name="username">
        <input type="password" name="password">
        ...
        <input type="submit" name="_submit" value="Login">
    </form>
</div>
```