---
title: Pagination Class
category: Advanced
order: 3
---


Pagination can be used with search.
The mandatory field you must send is the query string:

* page
* length

for example: `http://localhost/api/test?page=1&length=10`

**PHP Guide**

```php
$length = 10;
$sql = "SELECT * FROM ...";

$paginate = new Paginations();
$paginate->SetLength($length);
$paginate->SetQuery($sql);

return $paginate->GetDataPaginations(function ($result) {
    foreach ($result as $key => $val) {}
    return $result;
});
```

JSON Response

```json
{
    "page": 1,
    "totalpage": 2,
    "length": 10,
    "displayed": 10,
    "anchor": [
        {
            "page": 1
        },
        {
            "page": 2
        }
    ],
    "totaldata": 15,
    "data": []
}
```


