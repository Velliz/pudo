---
title: Service
category: Basics
order: 5
---

Service dinyatakan ketika sebuah kelas controller menurunkan kelas Service.

```php
class nilai extends Service {
```

Perbedaanya adalah pada return data. Alih-alih mencari halaman html dan merendernya, Serive akan langsung membuat representasi data JSON dari return yang dihasilkan function.
Namun, tentu dengan beberapa atribut tambahan yang ditambahkan secara otomatis.

* time   - server execution time.
* status - biasanya terdiri dari **success** atau **failed**.
* data   - disini data dari return function terletak.
* token  - adalah data tambahan yang berfungsi untukperlindungan dari serangan CSRF.
```json
{
  "time": 0.0010089874267578,
  "status": "success",
  "data": {
    "token": "356cb1c5693c6481e08599b553e50c25b43aca30fbed5ad877a319f6eb7d7a42"
  }
}
```

Contoh, jika anda mempunyai controller dengan return function berikut.

```php
public function siswa() {
    return array(
        'NIK' => '1266409',
        'Nama' => 'Didit Velliz',
        'Usia' => 22,
        'Keahlian' => array(
            'PHP', 'MySQL'
        )
    );
}
```

Maka json yang dihasilkan ketika halaman tersebut di buka adalah.

```json
{
  "time": 0.33715486526489,
  "status": "success",
  "data": {
    "NIK": "1266409",
    "Nama": "Didit Velliz",
    "Usia": 22,
    "Keahlian": [
      "PHP",
      "MySQL"
    ],
    "token": "356cb1c5693c6481e08599b553e50c25b43aca30fbed5ad877a319f6eb7d7a42"
  }
}
```