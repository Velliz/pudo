---
title: Nginx
category: Web Server
order: 3
---

Anda dapat mengatur *clean url* dengan nginx dengan konfigurasi ```nginx.conf```
berikut

```text
server {
    listen   8000;
    server_name  localhost;

    client_max_body_size  100m;

    root   /home/www_puko;
    index index.php index.html index.htm;

    location = /favicon.ico {
        access_log off;
        log_not_found off;
    }

    location = /robots.txt {
        access_log off;
        log_not_found off;
    }

    location ~* (\.css|\.js|\.png|\.jpg|\.gif|robots\.txt|\.eot|\.ttf|\.woff)$ { 
        add_header Access-Control-Allow-Origin *;
    }
  
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location / {
        rewrite ^/(.*)$ /index.php?request=$1 last;
        try_files $uri $uri/ =404;
    }

}
```

Jika ingin mengatur *reverse proxy* anda dapat menggunakan sample berikut:

```text
server
{
  server_name anywhere.com;
  location /
  {    
    proxy_pass  http://localhost:8000;
    include conf.d/proxy_header;
  }
}
```

Template *proxy_header*

```text
### force timeouts if one of backend is died ##
proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;

set	$scheme_to_sn	"://";
set	$after_sn	"/";
 
### Set headers ####
proxy_set_header	Accept-Encoding	    "";
proxy_set_header	Host			    $host;
proxy_set_header	X-Proxy-Target	    $proxy_host;
proxy_set_header	X-Proxy-Port	    $proxy_port;
proxy_set_header	X-Real-IP		    $remote_addr;
proxy_set_header	X-Forwarded-For	    $proxy_add_x_forwarded_for;
proxy_set_header	X-Forwarded-Proto	$scheme;
proxy_set_header	X-Gateway		    $server_addr;
proxy_set_header	X-Development-Server	"true";
proxy_set_header	X-Server-Name		$server_name;
proxy_set_header	X-Site-For		    "";
proxy_set_header	X-Source-Access	    "internal";
proxy_set_header	App-Base-URI		$scheme$scheme_to_sn$server_name$after_sn;
		
add_header		    Front-End-Https on;

proxy_redirect		off;

proxy_no_cache 		$cookie_PHPSESSID;
proxy_cache_bypass 	$cookie_PHPSESSID;
```