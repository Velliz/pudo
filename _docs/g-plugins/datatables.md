---
title: DataTable Class
category: Plugins
order: 4
---

**PHP Guide**

DataTable is the most popular jQuery plugin used to display data in table.
Puko provides libs that can simplify the use of DataTable, especially when using
Datatable Serverside / Server Processing. 

To get started, create an object from the DataTable class with the following syntax:

```php
$table = new DataTables(DataTables::POST);
```

Then define your columns, especially the column names that are *selected* from the database.

```php
$table->SetColumnSpec(array(
    "name",
    "age",
    "address",
    "email"
));
```

After that, you must write a *sql* query to be processed later by the DataTable class.

```php
$table->SetQuery("SELECT * FROM students;");
```

Then, you can display the data using the following syntax.

```php
return $table->GetDataTables(function ($result) {
    foreach ($result as $key => $val) {
        //you can perform modification data results here
    }
    return $result;
});
```

Note that the **GetDataTables** function uses *callbacks* in the form of anonymous *functions*.
This feature is useful if you want to perform data transformation before the result *select*
shown.

**JavaScript Guide**

Make sure you have the required DataTables js files and import them correctly into the html file.
This is example for pte import syntax:

```html
{!js(<script src="assets/js/jquery.dataTables.min.js"></script>)}
{!js(<script src="assets/js/dataTables.bootstrap.min.js"></script>)}
```

> Attention: it is recommended to use DataTables version 1.10 or later.

Make sure you also have forwarded the file to the master template.
Usually, in the master template there will be the following input tags.

```html
<html>
    <head>...</head>
    <body>
    ...
    {CONTENT}
    ...
    {!part(css)}
    {!part(js)}
    </body>
</html>
```

Then, you can add JavaScript code instantiations of DataTables as shown below.

```javascript
let table = $('#example').DataTable({
    ajax: {
        type: "POST",
        dataType: "json",
        responsive: true,
        url: $('base#api').attr('href') + "backend/api/endpoint",
        data: function (data) {

        },
        error: function (jqXHR, textStatus, errorThrown) {
            console.log(errorThrown);
        },
        dataSrc: function (json) {
            if (json.exception !== undefined) {
                return [];
            }
            return json.data;
        }
    },
    processing: true,
    serverSide: true,
    lengthMenu: [
        [10, 50, 100, 250, 350, 500],
        ['10', '50', '100', '250', '350', '500']
    ],
    dom: 'Bfrtip',
    buttons: [
        {
            extend: "pageLength",
            className: "btn-sm"
        },
        {
            extend: "copy",
            className: "btn-sm"
        },
        {
            extend: "csv",
            className: "btn-sm"
        },
        {
            extend: "excel",
            className: "btn-sm"
        },
        {
            extend: "pdfHtml5",
            className: "btn-sm"
        },
        {
            extend: "print",
            className: "btn-sm"
        },
        {
            text: 'Custom Button',
            className: "btn-sm",
            action: function ( e, dt, node, config ) {

            }
        }
    ],
    initComplete: function (settings, json) {

    },
    rowCallback: function (row, data) {

    },
});
```

> Note: the number of *orderable* in *columns* must be the same as *SetColumnSpec* in your PHP code.
