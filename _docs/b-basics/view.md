---
title: View
category: Basics
order: 4
---

View in puko is divided into master layout and hierarchical content generated automatically when you execute
console command `php puko routes view add ...`. The most important thing you should know in first is: '_View part in puko don't have logic_'.
Role model of view in puko is enough for render data, also render data in list with loop tags.

> As the view layer in HMVC should do their job to **Presenting Data**. 
> You can utilize the full potential of JavaScript if want to build rich animation or logic in view. 

As *default* when *Puko* installed with composer you have this `master.html` file as starting point of view:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{!title}</title>
    <style>
        body {
            background-color: #039BE5;
            color: white;
        }
    </style>
</head>
<body>
<div>
    {CONTENT}
</div>
<br>
<br>
{!part(css)}
{!part(js)}
</body>
</html>
```

> Utilize pure html file. So the file cannot disrupted with php syntax when the file grow bigger.

As you can see Puko have a template syntax tag like `{!title}` `{CONTENT}` `{!part()}`. This called PTE tag.
If you want to know more about the PTE tag, you can see the official project and documentation [here](https://github.com/Velliz/pte). 

Let's describe what that tag is doing in our html file:

* Tag `{!title}`

This tag used for rendering atomic data. In this case the tag will render value from variables called **title**.
 
* Tag `{CONTENT}`

This tag will load the content html file in runtime.

* Tag `{!part(css)}`

This tag will place the css file declared form content html file.

* Tag `{!part(js)}`

This tag will place the JavaScript file declared form content html file.

You also can have more than one master html file. 
This is useful when you need different template layout for different user roles for examples:

```text
master.html
master-admin.html
master-guest.html
master-owner.html
```

Besides the master html file. There is also _hierarchical content_ placed in same structure as routing definitions.
This synchronization and restrictions applied to enforce HMVC always implemented in the right way. 
So when you make a view routing like this:

`php puko routes view add accounts/user/{?}/links`

```text
controller     : accounts\user
function       : links
accept         : get,post
```

So you can find the html file in this hierarchical folder structure:

```text
- assets/
  - html/
    - id/
      - accounts/
        - user/
          - links.html
```

Controller file

```text
- controller/
  - accounts/
    - user.php
```

Now, what about when you have a master html file more than one file? 
You can create a new controller and easily switch between them with this command:

```php
/**
 * #Master master-admin.html
 */
class user extends View {
    
    public function links() {
    
    }
}
```

> Note: if the **#Master master-admin.html** command not declared. Puko will automatically reffer the default **master.html**