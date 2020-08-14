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

```text
config/routes.php
controller/member/reports.php
```

If the routes clause was `view` puko will also update and auto-generated these files:

```text
assets/html/en/member/reports/pages.html
assets/html/id/member/reports/pages.html
```

You can also see all registered routes with this command:

```text
php puko routes list
```

> All generated routes stored in `config/routes.php`

If you want to update or modify the HTTP verb accepted from the Routing url registered, 
you can update it with command:

```text
php puko routes view update member/{?}/reports
```

Apply your revision when answering items asked.

---

Puko also can remove unused routes with remove command:

```text
php puko routes view remove member/{?}/reports
```

> For security concerns puko not deleting the .php and .html file. You must review and remove it manually.