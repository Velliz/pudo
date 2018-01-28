---
title: View
category: Basics
order: 4
---

View pada *Puko* diatur dengan sistem master dan content, master terletak di dalam folder *assets/master* 
sedangkan content lokasinya mengikuti tata letak controller yang *file*-nya sudah otomatis di buat saat *Scaffolding* Routes.
Secara *default* ketika anda memulai sebuah proyek baru dengan *Puko*. 
Anda akan memiliki satu buah file bernama master.html yang berfungsi sebagai awal dengan struktur *file* berikut ini.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{!title}</title>
</head>
<body>
<div>
{CONTENT}
</div>
{!part(css)}
{!part(js)}
</body>
</html>
```

> Perhatian: tag dapat anda lihat secara lengkap pada sesi tutorial **Puko Template Engine**.

Jika diperhatikan, maka anda akan menemukan tag dengan dua jenis kerangka, {!} dan {CONTENT}.

```text
{CONTENT}
```

CONTENT berfungsi sebagai pewadah tempat diletakannya content html nantinya.

```text
{!part(css)}
{!part(js)}
```

part() berfungsi sebagai pewadah tempat diletakannya assets.

Anda juga dapat membuat beberapa *file* master selain master.html

```text
master.html
master-admin.html
master-guest.html
master-siswa.html
```

Selain master, terdapat juga content yang seperti disinggung diawal, 
lokasinya mengikuti tata letak controller yang *file*-nya sudah otomatis di buat saat *Scaffolding* Routes.
Jadi, jika anda membuat routes dengan format berikut.

```text
php puko routes view add akun/tautan

controller     : akun\user
function       : profile
accept         : GET,POST
```

Maka anda akan menemukan file content anda pada direktori berikut.

```text
- assets/
  - html/
    - id/
      - akun/
        - user/
          - profile.html
```

```text
- controller/
  - akun/
    - user.php
```

Untuk mengatur master apa yang hendak digunakan pada sebuah content, anda dapat mengaturnya melalui controller.

```php
/**
 * #Master master-siswa.html
 */
class user extends View {
    
    public function profile() {
    
    }
}
```

> Perhatian: jika anda tidak mendefinisikan **#Master master-siswa.html** maka secara otomatis controller akan mencari master default yaitu **master.html**