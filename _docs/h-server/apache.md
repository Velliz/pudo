---
title: Apache
category: Web Server
order: 2
---

You can set *clean url* with apache with the following `.htaccess` configuration:

```text
<IfModule mod_rewrite.c>

RewriteEngine On

RewriteCond %{REQUEST_URI} !(public|css)
RewriteCond %{REQUEST_URI} !(\.css|\.js|\.png|\.jpg|\.gif|robots\.txt)$ [NC]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule  ^(.+)?$ index.php?request=$1&lang=$2 [L,QSA]

</IfModule>
```
