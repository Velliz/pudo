---
title: Docker
category: Web Server
order: 5
---

Configuration template for ```Dockerfile```


```bash
FROM alpine:3.11

# Install packages
RUN apk --no-cache add php7 php7-session php7-fpm php7-pdo php-pdo_mysql \
    php7-mysqli php7-json php7-openssl php7-curl php7-zlib php7-xml \
    php7-phar php7-intl php7-dom php7-xmlreader php7-ctype \
    php7-mbstring php7-gd php7-soap php7-ldap nginx supervisor curl git

# Configure nginx
COPY bootstrap/nginx.conf /etc/nginx/nginx.conf

# Configure PHP-FPM
COPY bootstrap/fpm-pool.conf /etc/php7/php-fpm.d/zzz_custom.conf
COPY bootstrap/php.ini /etc/php7/conf.d/zzz_custom.ini

# Configure supervisord
COPY bootstrap/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Add application
RUN mkdir -p /var/www/html
WORKDIR /var/www/html
COPY . /var/www/html/

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN composer install

EXPOSE 80 443
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
```

Template ```supervisord.conf```

```bash
[supervisord]
nodaemon=true

[program:php-fpm]
command=php-fpm7 -F
stdout_logfile=/dev/stdout
stdout_logfile_maxbytes=0
stderr_logfile=/dev/stderr
stderr_logfile_maxbytes=0
autorestart=false
startretries=0

[program:nginx]
command=nginx -g 'daemon off;'
stdout_logfile=/dev/stdout
stdout_logfile_maxbytes=0
stderr_logfile=/dev/stderr
stderr_logfile_maxbytes=0
autorestart=false
startretries=0
```

Template ```php.ini```

```bash
[Date]
date.timezone="Asia/Jakarta"

[Memory]
memory_limit=512M

[Upload]
upload_max_filesize=50M
```

Template ```nginx.conf```

```bash
worker_processes  1;
pid /run/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main_timed  '$remote_addr - $remote_user [$time_local] "$request" '
                            '$status $body_bytes_sent "$http_referer" '
                            '"$http_user_agent" "$http_x_forwarded_for" '
                            '$request_time $upstream_response_time $pipe $upstream_cache_status';

    access_log /dev/stdout main_timed;
    error_log /dev/stderr notice;

    keepalive_timeout  65;

    server {
        listen [::]:80 default_server;
        listen 80 default_server;
        server_name _;

        client_max_body_size 50M;
        sendfile on;

        root /var/www/html;
        index index.php index.html;

        location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to index.php
            rewrite ^/(.*)$ /index.php?request=$1 last;
            try_files $uri $uri/ =404;
        }

        location = /favicon.ico {
            access_log off;
            log_not_found off;
        }

        location = /robots.txt {
            access_log off;
            log_not_found off;
        }

        # redirect server error pages to the static page /50x.html
        #
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
            root /var/lib/nginx/html;
        }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
            try_files $uri =404;
            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_pass  127.0.0.1:9000;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param SCRIPT_NAME $fastcgi_script_name;
            fastcgi_index index.php;
            include fastcgi_params;
        }

        location ~* \.(jpg|jpeg|gif|png|css|js|ico|xml|xls|xlsx|svg|doc|docx|txt|ttf|eot|woff)$ {
            add_header Access-Control-Allow-Origin *;
            expires 5d;
        }

        # deny access to . files, for security
        #
        location ~ /\. {
            log_not_found off;
            deny all;
        }
    }
}
```

Template ```fpm-pool.conf```


```bash
[global]
; Log to stderr
error_log = /dev/stderr

[www]
; Enable status page
pm.status_path = /fpm-status

; Ondemand process manager
pm = ondemand

; The number of child processes to be created when pm is set to 'static' and the
; maximum number of child processes when pm is set to 'dynamic' or 'ondemand'.
; This value sets the limit on the number of simultaneous requests that will be
; served. Equivalent to the ApacheMaxClients directive with mpm_prefork.
; Equivalent to the PHP_FCGI_CHILDREN environment variable in the original PHP
; CGI. The below defaults are based on a server without much resources. Don't
; forget to tweak pm.* to fit your needs.
; Note: Used when pm is set to 'static', 'dynamic' or 'ondemand'
; Note: This value is mandatory.
pm.max_children = 50

; The number of seconds after which an idle process will be killed.
; Note: Used only when pm is set to 'ondemand'
; Default Value: 10s
pm.process_idle_timeout = 10s;

; The number of requests each child process should execute before respawning.
; This can be useful to work around memory leaks in 3rd party libraries. For
; endless request processing specify '0'. Equivalent to PHP_FCGI_MAX_REQUESTS.
; Default Value: 0
pm.max_requests = 500

; Make sure the FPM workers can reach the environment variables for configuration
clear_env = no

; Catch output from PHP
catch_workers_output = yes
```
