---
title: Vagrant
category: Web Server
order: 4
---

Configuration file for `Vagrantfile`

```bash
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Box Settings
  config.vm.box = "ubuntu/trusty64"
  config.vm.boot_timeout = 600

  # Provider Settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 700
    vb.cpus = 2
    vb.name = "puko"
  end

  # Network Settings
  config.vm.network "private_network", ip: "192.168.33.10", auto_correct: true

  # Database Settings
  config.vm.network "forwarded_port", guest: 3306, host: 3306, auto_correct: true

  # Folder Settings
  config.vm.synced_folder ".", "/home/www_app", :nfs => { :mount_options => ["dmode=777", "fmode=666"] }

  # Hosts Settings
  if defined?(VagrantPlugins::HostsUpdater)
    config.vm.hostname = "puko.com"
    config.hostsupdater.aliases = [
      "www.puko.com"
    ]
  end

  # Provision Settings
  config.vm.provision "shell", path: "bootstrap.sh"
end
```

Provisioning with ```bootstrap.sh```

```bash
# Update Packages
apt-get update
# Upgrade Packages
apt-get upgrade

# Basic Linux Stuff
apt-get install -y git

# Apache
apt-get install -y nginx

#Add Onrej PPA Repo
apt-add-repository ppa:ondrej/php
apt-get update

# Install Memcached
apt-get install memcached

# Install PHP
apt-get install -y php7.2

# PHP Mods
apt-get install -y php7.2-common
apt-get install -y php7.2-cli
apt-get install -y php7.2-cgi
apt-get install -y php7.2-soap
apt-get install -y php7.2-curl
apt-get install -y php7.2-fpm
apt-get install -y php7.2-zip
apt-get install -y php7.2-gd
apt-get install -y php7.2-json
apt-get install -y php7.2-ldap
apt-get install -y php7.2-mcrypt
apt-get install -y php7.2-mbstring
apt-get install -y php7.2-xml
apt-get install -y php7.2-xmlrpc
apt-get install -y php7.2-memcached
apt-get install -y php7.2-zip

# Install Composer
curl -Ss https://getcomposer.org/installer | php
sudo mv composer.phar /usr/bin/composer

# Set MySQL Pass
debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'

# Install MySQL
apt-get install -y mysql-server

# PHP-MYSQL lib
apt-get install -y php7.2-mysql

# Configure host
cat << 'EOF' > /etc/nginx/sites-available/default
server {
	# Port that the web server will listen on.
	listen 80;

	# Host that will serve this project.
	server_name localhost;

    # Client body size
	client_max_body_size  100m;

	# The location of our projects public directory.
	root /home/www_app;

	# Point index to the Laravel front controller.
	index index.php index.html;

	location = /favicon.ico {
        access_log off;
        log_not_found off;
    }

    location = /robots.txt {
        access_log off;
        log_not_found off;
    }

    location ~* (\.css|\.js|\.png|\.jpg|\.gif|robots\.txt|\.eot|\.ttf|\.woff|\.xlsx)$ {
        add_header Access-Control-Allow-Origin *;
    }

    location ~ \.php$ {
        try_files $uri =404;
        include /etc/nginx/fastcgi_params;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location / {
        rewrite ^/(.*)$ /index.php?request=$1 last;
        try_files $uri $uri/ =404;
    }

}
EOF

# Restart Service
sudo service nginx restart
```

Additional steps for make MySQL can have *remote access*

```bash
vagrant ssh

vim /etc/mysql/my.cnf

bind-address = 127.0.0.1

:w !sudo tee %

mysql -u root -p

GRANT ALL PRIVILEGES ON *.* TO `root`@`%` IDENTIFIED BY 'root' WITH GRANT OPTION;

FLUSH PRIVILEGES;

exit;

sudo service mysql restart
```
