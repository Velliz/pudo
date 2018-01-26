---
title: Configuration
category: Getting Started
order: 2
---

Untuk memulai mengerjakan sebuah project *Puko Framework* menyediakan beberapa command khusus untuk
memudahkan pembuatan project.
command yang dapat anda gunakan yaitu:

**Konfigurasi Database**

```text
php puko setup db
```

Anda akan diminta untuk membubuhkan hostname, port, username, password dan database name.
Setup db akan menyimpan konfigurasi koneksi ke database anda di file *config/database.php*. 
Jika terhubung *Puko Framework* akan membuat base model otomatis dari skema database tersebut.

**Konfigurasi Enkripsi**

```text
php puko setup secure
```

Anda akan diminta untuk membubuhkan identifier, secure key, dan cookies name untuk melakukan enskripsi pada project
dan cookies yang digunakan.
