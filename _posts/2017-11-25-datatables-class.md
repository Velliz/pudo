---
layout: page
title: "DataTables Class"
category: ref
date: 2017-11-25 14:26:14
---

```php
$data = new DataTables();
$data->SetColumnSpec(array(
    "column1",
    "column2",
    "column3",
    "column4",
));
$data->SetQuery("");

echo $data->GetDataTables(function ($result) {
    foreach ($result as $key => $val) {
        //modify data results here
    }
    return $result;
});
```
