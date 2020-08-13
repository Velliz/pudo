---
title: Routing
category: Basics
order: 1
---

Until now, Puko framework have 3 different kind of routing clause as-is controller functionality, 
we call it `view`, `service`, and `console`. You can see about [controller](/pudo/b-basics/controller/) to see further what that means.
Puko can scaffolds Routing process with `pukoconsole` tools included as dev-dependency.

To add Routing, you can type in _console/terminal/powershell_:

```text
php puko routes <controller_clause> add <rest_style_urls>
```

> rest_style_urls can typed with {?} to identify it as dynamic PHP GET parameters.

For example:

```text
php puko routes view add member/{?}/reports
```

Items asked:

|Items|Description|Examples|
|---|---|---|
|Controller name|File name. You can use \ to place the file in sub-directories|member\reports|
|Function name|Function name|pages|
|Accept?|HTTP verb GET,POST,PUT,PATCH,DELETE multiple by commas|get,post|

> You must using (\) _backslash_ for separating controller.

After completed, puko is updating and auto-generated these files:

```
assets/html/en/member/reports/pages.html
assets/html/id/member/reports/pages.html
config/routes.php
controller/member/reports.php
```

---

Serta perubahan pada Routing yang anda buat dengan sintaks *update* atau *delete* dengan perintah.

```text
php puko routes service update ...
```

```text
php puko routes service delete ...
```

Anda juga dapat melihat seluruh Routes yang telah terdaftar dengan perintah.

```text
php puko routes view list
```

Anda juga dapat melihat semua konfigurasi yang telah dibuat oleh console tersimpan di dalam file routes.php yang berada dalam folder *config*

```php
$routes = [
    "router" => [],
    "error" => [
        "controller" => "error",
        "function" => "display",
        "accept" => [
            "GET",
            "POST"
        ]
    ],
    "not_found" => [
        "controller" => "error",
        "function" => "notfound",
        "accept" => [
            "GET",
            "POST"
        ]
    ],
    "maintenance" => [
        "controller" => "error",
        "function" => "maintenance",
        "accept" => [
            "GET",
            "POST"
        ]
    ]
];
return $routes;
```