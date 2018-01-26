---
title: Database
category: Basics
order: 6
---

*Puko Framework* menggunakan PDO sebagai database wrapper dan menyimpan pengaturan database pada file *config/database.php*
dengan konfigurasi default

```php
return array(
    'dbType' => 'mysql',
    'host' => 'localhost',
    'user' => 'root',
    'pass' => '',
    'dbName' => '',
    'port' => 3306
);
```

Anda dapat merubah file ini sesuai dengan konfigurasi database yang anda gunakan.
Anda juga dapat melakukan konfigurasi otomatis melalui command prompt dengan perintah

```text
php puko setup db
```