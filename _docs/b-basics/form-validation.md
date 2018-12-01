---
title: Form dan Validasi
category: Basics
order: 8
---

**Form HTML**

Form adalah salah satu cara yang umum digunakan untuk mengirim data dari user ke aplikasi web.
Pada *Puko* form memiliki dua rekomendasi tambahan agar data dapat diproses dengan aman di controller.
Tambahan tersebut yaitu.

```html
<input type="hidden" name="token" value="{!token}" />
```

Dan sebuah *flag* untuk mengindikasikan form tersebut adalah *post data* dan dapat ditulis dengan dua cara.

```html
<input type="submit" name="_submit" value="kirim" />
```

```html
<input type="hidden" name="_submit" value="_submit" />
```

Berikut ini contoh sebuah *form* login.

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

> Perhatian: **action=""** mengindikasikan bahwa pengiriman dilakukan ke alamat url diri sendiri.

Untuk melakukan pengambilan nilai, anda dapat menggunakan perntah berikut.

```php
if (Request::IsPost()) {
    $username = Request::Post('username', null);
    $password = Request::Post('password', null);
}
```

Jika diperhatikan, sintaks **Request::Post()** mempunyai dua parameter, yaitu nama kiriman dari form dan *null* sebagai parameter kedua.
*null* disini bertindak sebagai *default value* jika data gagal diambil dari form.

Sedangkan **Request::IsPost()** berfungsi untuk mengecek nilai dari token untuk menilai apakah kiriman data sah atau berupa serangan CSRF.
Request juga memiliki beberapa varian lain, diantaranya.

```php
Request::Get('username', null);
```

```php
Request::Cookies('username', null);
```

```php
Request::Vars('username', null);
```

```php
Request::Files('username', null);
```

**Form AJAX**

Pertama, anda perlu menyimpan token secara tersembunyi pada halaman html. Seperti contoh berikut.

```html
<input type="hidden" name="token" value="{!token}" />
```

Lalu membuat AJAX secara terpisah pada file *JavaScript*. Berikut ini contoh sebuah kerangka jQuery *AJAX*.

```javascript
$.ajax({
    url: "",
    type: "POST",
    data: {
        username: $('input[name=username]').val(),    
        password: $('input[name=password]').val(),    
        token: $('input[name=token]').val(),    
        _submit: 'submit'    
    },
    dataType: "json",
    success: function(data) {
        //kode tambahan jika sukses
    }
});
```

**Validasi**

Coming Soon