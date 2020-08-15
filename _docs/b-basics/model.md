---
title: Model
category: Basics
order: 3
---

Let's get to know about model. The (M) layer of puko framework HMVC pattern.
This part of puko has responsible to connecting your app with a database 
or multiple database for Create, Read, Update and Delete operations.
Database in puko handled by the DataBase Interface (DBI) singleton objects.

But, before that, we need setup a database connections. To summarize the process we often using `pukoconsole` command:

```
php puko setup db
```

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

What this process means?

Puko will save the connection setting in `config/database.php` file 
and generate corresponding PHP class model as **data object wiring** with your database model.
Those files generated and saved in `plugins/model/<schema>` directory.

> That file should not be modified

So, why we need **data object wiring**?

At concept level, data object wiring inspired by Data Access Object (DAO) patterns 
but only implement the wiring mechanism to keep it small and simple.
And because we usually don't remember clearly the column on database entity. 
So with object wiring you now have clues about your column on the database in case you forget.
Especially when used with good IDE, those tools can provide auto-completions trough your data.
Enough theory, let's see it in action.

Assumed you have basic knowledge on MySQL and have a database table `inventory` and you already done executing setup db command above.
This is example of what inside table `inventory`:

|id|name|created|descriptions|
|---|---|---|---|
|1|Chair|2020-08-15|Minimalist chair made from pine woods|
|2|Laptop|2020-08-16|Gaming notebooks with core i7 and RTX2070 Max-Q|

> Alert: tables name must only contain letters without special character or space due to limitations of php class name rules.

Create or save operations:

```php
$inventory = new plugins\model\primary\inventory();
$inventory->id = $_POST['id'];
$inventory->name = $_POST['name'];
$inventory->created = date('Y-m-d H:i:s');
$inventory->descriptions = $_POST['descriptions'];

$inventory->save();
```

Read operations:

```php
$inventory = new plugins\model\primary\inventory(1);

echo (array) $inventory;
```

Update or modify operations:

```php
$inventory = new plugins\model\primary\inventory(1);
$inventory->id = $_POST['id'];
$inventory->name = $_POST['name'];
$inventory->created = date('Y-m-d');
$inventory->descriptions = $_POST['descriptions'];

$inventory->modify();
```

Delete or remove operations:

```php
$inventory = new plugins\model\primary\inventory(1);

$inventory->remove();
```

Get all data:

```php
$all = plugins\model\primary\inventory::GetAll();
```

As you can see. Basic CRUD operations is simple and don't need to use any manual typed SQL query.

> The DataBase Interface (DBI) in puko framework for now only support MySQL and MariaDB. 

But then how about run the stored procedure or executing complex query like join operations?

For executing stored procedure you can follow this example:

```php
DBI::Call('stored_procedure_name', [
    $parameter1, $parameter2
]);
```

For complex query you can extends the model classes and implement **ModelContracts** in order to have uniformity.
Let's see by example:

Create new php file: `model/InventoryModel.php`

```php
class InventoryModel extends inventory implements ModelContracts {
```

The **ModelContracts** interface will be forcing you to implement 9 abstract method.

`GetData()` This method should return data available on the database in array structure

`GetById($id)` This method should return one row from database specified by id

`IsExists($id)` This method should return true if row found or false if not found from database specified by id

`IsExistsWhere($column, $value)` This method should return true if row found or false if not found from database specified by custom selection

`GetDataSize()` This method should return count of the data on the database

`GetDataSizeWhere($condition)` This method should return count of the data on the database with selected conditions

`GetLastData()` This method should return last inserted data

`SearchData($keyword)` This method should return search result data available on the database in array structure

`GetDataTable($condition)` This method should return search result data available on the database in datatables json format

These pre-defined method above created to give developer the start point. 
Puko framework have this to offer consistency and because most database operation can handled by these pre-defined method. 
Let's see it through sample code:

InventoryModel.php

```php
public static function SearchData($keyword = []) {
    $strings = "";
    foreach ($keyword as $column => $values) {
        $strings .= sprintf(" AND (%s = '%s') ", $column, $values);
    }

    $sql = sprintf("SELECT i.id, i.created, i.name, i.descriptions
    FROM inventory i
    WHERE (i.created IS NOT NULL) %s;", $strings);

    return DBI::Prepare($sql)->GetData();
}
```

```php
//now we using InventoryModel. Our custom class that extends inventory plugin model.
$inventoru = InventoryModel::SearchData([
    'created' => '2020-08-14'
]);
```

Why puko have this type of interface? The goal is uniformity. But keep in mind it's optional,
you can have your own way to work with the databases.

---

**DBI**

You already know how to do CRUD operations with **data object wiring**. This section will explain with code sample
another set of feature available in DBI.

* `Prepare`

To pass your sql query into DBI classes.

```php
$sql = "SELECT * FROM inventory WHERE (id = @1);";
$response = DBI::Prepare($sql);
```

* `GetData()`

Used to retrieve all data from the database in arrays indexed format. Prepared statement is also available.
You can se it from example below:

```php
$sql = "SELECT * FROM inventory WHERE (id = @1);";
$response = DBI::Prepare($sql)->GetData($id);
```

```php
$sql = "SELECT * FROM inventory WHERE (id = @1) AND (name = @2);";
$response = DBI::Prepare($sql)->GetData($id, $name);
```

```php
$sql = "SELECT * FROM inventory WHERE (id = @1) AND (name = @2) AND (created = @3);";
$response = DBI::Prepare($sql)->GetData($id, $name, $created);
```

* `FirstRow()`

As `GetData()` but only retrieve 1 row data in single array formats. Prepared statement is also available.
You can se it from example below:

```php
$sql = "SELECT * FROM inventory WHERE (id = @1) LIMIT 1;";
$response = DBI::Prepare($sql)->FirstRow();
```

* Run()

For executing query. Usually used for executing stored procedure and non select query.

```php
$sql = "UPDATE inventory SET name = 'Laptop Ultrabooks' WHERE (id = @1);";
$response = DBI::Prepare($sql)->Run($id);
```