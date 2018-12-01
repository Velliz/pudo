---
title: Deploy
category: Getting Started
order: 3
---

Anda dapat menjalankan *Puko* dengan berbagai cara.

* Tanpa web server

Gunakan *command* berikut ini untuk menjalankankannya langsung.

```text
php puko serve ...
```

Anda dapat mengisikan ... dengan port yang diinginkan.

```text
php puko serve 4000
```

Maka, anda dapat membukanya pada halaman web.

```text
localhost:4000
```

* Apache Web Server

Gunakan konfigurasi *.htaccess* berikut untuk menjalankan puko framework dengan Web Server Apache.

```apacheconfig
<IfModule mod_rewrite.c>

RewriteEngine On

RewriteCond %{REQUEST_URI} !(public|css)
RewriteCond %{REQUEST_URI} !(\.css|\.js|\.png|\.jpg|\.gif|robots\.txt)$ [NC]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule  ^(.+)?$ index.php?request=$1&lang=$2 [L,QSA]

</IfModule>
```

* Nginx 

Coming Soon