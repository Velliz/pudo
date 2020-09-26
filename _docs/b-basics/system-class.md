---
title: System Class
category: Basics
order: 8
---

### Global State

* Error Display

Page to this template located at `assets/html/id/error/display.html` and the controller file `controller/error.php at function display()`
and triggered because the http accept don't match with the verb opened from web browser.
For example routes registered with verb *POST* and you access the routes with verb *GET*.
This error will execute immediately.

* Error Maintenance

This page displayed if the index variable called `environment` switched to 'MAINTENANCE'.
This will take down website and will response Under Maintenance info on the screen.
You can customize the look of error page at `assets/html/id/error/maintenance.html` and the controller file `controller/error.php at function maintenance()`

* Error Not-Found

This page displayed when not-exists routes opened.
You can customize the look of not found page at `assets/html/id/error/notfound.html` and the controller file `controller/error.php at function notfound()`

> These page displayed if the error controller class `error.php` set to extend the View middleware.

---

### Function & Doc Command State

* Not Authenticated

Triggered when function issued with doc command: `#Auth bearer true` when user not authenticated, the error raised.
You can customize the look of not authenticated page at `system/auth.html`.
No controller file available for this.

* Under Construction

Triggered when function issued with doc command: `#UnderConstruction true` the error raised.
You can customize the look of not authenticated page at `system/construction.html`.
No controller file available for this.

* Error

This error occurs when an error inside controller function triggered, like not assigned variable being echoed. (*caused undefined variable error)
You can customize the look of not authenticated page at `system/error.html`.
No controller file available for this.

* Exception

This error occurs when an `throw new Exception()` executed.
You can customize the look of not authenticated page at `system/exception.html`.
No controller file available for this.

* Not Authorized for Permission

This error occurs when an `#Permission \pukoframework\auth\Bearer@\plugins\auth\UserAuth permissions@MANAGER` executed.
You can customize the look of not authenticated page at `system/permission.html`.
No controller file available for this.

> All html template only available when you extend the controller class to View middleware.