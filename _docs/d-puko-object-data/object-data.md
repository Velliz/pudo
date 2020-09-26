---
title: Basic CRUD
category: Puko Object Data
order: 1
---

Puko framework primarily makes use of `plugins\model` object instantiation to perform CRUD processing.
This feature called Object Data. 
In order to see how this Data Object works, you can look at the following syntax example:

```php
$bibit = new bibit_pohon();
$bibit->harga = 35000;
$bibit->jenis_pohon = "Mangga Apel";
$bibit->jumlah = 5;
$bibit->ket = "Dari cangkokan super";

$bibit->save();
```

```php
$bibit->modify();
```

```php
$bibit->remove();
```

From the code snippet above we can see that:
* **bibit_pohon** is the intantiation of a class.
* **bibit_pohon** have properties in the form of _harga, jenis_pohon, jumlah_ and _ket_.
* **bibit_pohon** perform the data storage process by calling the `save()` function.

If you are curious about what the tree seed class itself looks like, then here's the code:

```php
<?php

namespace plugins\model;

use pukoframework\pda\DBI;
use pukoframework\pda\Model;

/**
 * #Table bibit_pohon
 * #PrimaryKey id
 */
class bibit_pohon extends Model
{
    
    /**
     * #Column id int(10)
     */
    var $id = null;

    /**
     * #Column jenis_pohon varchar(45)
     */
    var $jenis_pohon = null;

    /**
     * #Column jumlah int(5)
     */
    var $jumlah = null;

    /**
     * #Column harga int(8)
     */
    var $harga = null;

    /**
     * #Column ket varchar(225)
     */
    var $ket = null;

}
```

> Attention: you don't need to create this class because it is automatically generated in the scaffolding `php puko setup db`

The first part to pay attention to is the class declaration:

```php
/**
 * #Table bibit_pohon
 * #PrimaryKey id
 */
class bibit_pohon extends Model
```

Where there is a `#Table bibit_pohon` and `#PrimaryKey id` which shows that the class connected to a table in the database
with the name of the table **bibit_pohon** and have a primary key with the name of the column **id**. 

During the scaffolding process, the puko reads the data structure down to the column level.
We can also pay attention to the properties that are formed in the class:

```php
/**
 * #Column id int(10)
 */
var $id = null;
```

Using `#Column id int (10)` let the puko framework know that the variable associated with the same named column in the database.
So what's so interesting about this method?

* You can do CRUD processing without writing SQL queries.
* Create code Completion-able database fields in PHP code.
* Produces a clean and easy syntax.