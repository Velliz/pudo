---
title: Configuration
category: Getting Started
order: 2
---

**Encryption**

Encryption required to secure many aspects in our applications. Puko framework mostly using this to secure
user authentication data in several forms. Sessions, Cookies, and Bearer. Puko can scaffolds this process with
`pukoconsole` tools included as dev-dependency.

> Puko using AES-256-CBC as encryption algorithms

To start configure Encryption, you can type in _console/terminal/powershell_:

```text
php puko setup secure
```

Items asked:

|Items|Description|Examples|
|---|---|---|
|Identifier|String text uniquely identify your app|inventory|
|Secure key|Strong text like passwords|s-inventoryApp2020#**|
|Cookies name|String text for cookie name|inventory|
|Session name|String text for cookie name|inventory|
|Session expired|Session expired number (in days) or blank for infinity|30|
|Session expired display text|Display text|Login to continue|
|Error display text|Display text|You don't have access to this application|

> You can also configure it manually from `config/encryption.php`

---

**App**

App `config/app.php` used to hold read-only variable and later can retrieved in controller for usages.
App file structured as PHP array and consists 3 root identifier `const`, `cache` and `logs`.

* Const

You can register your constant in `const` sections of file. For example:

```text
<?php return [
    'const' => [
        'API' => 'https://localhost:3000/api/',
    ]
    ...
];
```

* Cache

By default, puko utilize memcached as cache driver. 
You can configure the connection settings here.

```text
<?php return [
    ...
    'cache' => [
        'kind' => 'MEMCACHED',
        'expired' => 100,
        'host' => 'localhost',
        'port' => 11211,
    ]
    ...
];
```

> cache implementation coming soon

* Logs

Puko utilize a custom hook and slack Incoming WebHooks for error reporting and by default set to false.
If you have slack accounts, you can setup a Incoming WebHook URL and paste it in slack url.
Then in the puko slack section, set the active state to true.

> custom hook is coming soon

---

**Database**

Database configurations located at `config/database.php` folder. You can specify more than one connection because
puko uses schema name for each connection string. Puko can scaffolds database configuration process with
`pukoconsole` tools included as dev-dependency.

> as version 1.1.6 puko only supports MySQL and MariaDB database engine

you can type in _console/terminal/powershell_:

```text
php puko setup db
```

or if you only refresh the database (without re-write the database configuration): `php puko refresh db`

Items asked:

|Items|Description|Examples|
|---|---|---|
|Database Type|only supports MySQL for now|mysql|
|Hostname|Databaase IP address|localhost|
|Port|Databaase port address|3306|
|Schema Name|Schema name as identifier for multiple database|primary|
|Database Name|Name of databases|inventory|
|Username|User databases|root|
|Password|Paassword databases|******|

> At the end wizard is asking for another connection you can answer with y/n

You can refer to database section for detailed information.

---

**Extending and customize your own config**

Puko framework can also create custom config file.
for example if you want to add RabbitMQ message queue you can create new `rabbitmq.php`

Add this code:

```text
<?php return [
    'username' => 'administrator',
    'password' => '*******',
    'host' => '192.16.60.31',
    'port' => '5678'
];
```

You can retrieve the value with this code snippet:

```php
//initialize config skeleton
$config = pukoframework\config\Config::Data('rabbitmq');

//retrieve the value
$config['username'];
$config['password'];
$config['host'];
$config['port'];
```

---

**Routes**

Routes located in `config/routes.php` and holds all routing information.
This file supposed as read-only because most of the puko routing done with `pukoconsole` tools included as dev-dependency.

You can refer to Routing section for detailed information.