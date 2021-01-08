---
title: Multi Database
category: Puko Object Data
order: 3
---

When database connection configured, You will notice it with schema labeled as `primary`. 
Puko labeled it for primary database connection to use when your code invokes CRUD operations.
You can connect to more than one database with different labels.

For example invoke a setup db with another schema label:

`php puko setup db`

```
Database Type (mysql, oracle, sqlsrv, mongo) :mysql
Hostname (Default: localhost) :localhost
Port (Default: 3306) :3306
Schema Name (primary) :dashboard <- notice here we use non primary label for multiple database connection
Database Name :dashboardbbn
Username :root
Password :*******
```
After database configuration executed, as in `config/database.php` you will notice that now connection
have 2 configurations:

```php
$db['primary'] = [
    'dbType' => 'mysql',
    'host'   => 'localhost',
    'user'   => 'root',
    'pass'   => '******',
    'dbName' => 'primary',
    'port'   => '3306',
    'cache'   => false,
];
$db['dashboard'] = [
    'dbType' => 'mysql',
    'host'   => 'localhost',
    'user'   => 'root',
    'pass'   => '******',
    'dbName' => 'dashboard',
    'port'   => '3306',
    'cache'   => false,
];
```

> Keep in mind: Schema Name must unique. You can add another connection as you needs.

### CRUD operations for non `primary` connections.

* Insert

```php
$object = new models(null, 'dashboard');
...
$object->save();
```

> 'dashboard' is the schema name configured from `config/database.php`

* Update

```php
$object = new models(20, 'dashboard');
...
$object->modify();
```

* DBI

```php
$result = DBI::Prepare($sql, 'dashboard')->GetData();
$result = DBI::Prepare($sql, 'dashboard')->FirstRow();
```
