---
title: Authentication
category: Basics
order: 6
---

First step to set up an *Authentication* features in Puko Framework is typing this command in console/terminal: 

```text
php puko setup auth <auth_name>
```

You can type any name related to the entity. ex: `StudentAuth`, `GuestAuth` and so on. 
You can have more than one auth features to.

For example the command should look like this:

```text
php puko setup auth StudentAuth
```

After the command executed *file class* will auto-generated and placed in _plugins/auth_ directory.

```text
- plugins/
  - auth/
    - StudentAuth.php
```

If you open the *file*, you can see bellow empty method:

```php
public function Login($username, $password)
{
    //todo: your custom login code here
}

public function Logout()
{
    //todo: create or clear log in databases
}

public function GetLoginData($id)
{
    //todo: return your user data here
}
```

That method supposed to be filled with your own custom Authentication implementation.

---

**Login($username, $password)**

For login, you can validate your username and password received from function param 
and validate trough models or CURL request.

```php
public function Login($username, $password)
{
    $student = model\primary\StudentModel::GetByUsernamePassword($username, $password);
    $dataToSecure = [
        "id" => $student['id'],
        "username" => $student['user'],
        "class" => $student['class']
    ];
    $permission = ["STUDENT"];
    return new PukoAuth($dataToSecure, $permission);
}
```

> login must return a PukoAuth class object.

Then, you can implement the login code on *controller* with the syntax like this example:

```php
$login = Session::Get(StudentAuth::Instance())->Login($username, $password);
```

**SiswaAuth::Instance()** is the object build automatic by puko to auto-wire the login process.

For `Session` and `Cookies`. If login process success. 
Then the **$login** variable assigned will have `true` value and `false` if the login process failed.

For `Bearer`. If the login process success.
Then the **$login** variable assigned will hold the string encrypted data.
If fails, **$login** variable will have *false*.

**Logout()**

This is logout callbacks. You can write any code to clean up the logout process. 

```php
public function Logout()
{
    //cleanup process here
    return true;
}
```

**GetLoginData($id)**

To validate an Authentication, you must decode back the encryption string generated on the login process.
So to simply that process, puko utilized an GetLoginData as callback function 
after decoding string information that hold 2 parameters. 
The first is `$secure` that contain all of `$dataToSecure` supplied in login process. 
Same to second `$permission` param, will contain all permission code supplied in login process.
 
```php
public function GetLoginData($secure, $permission)
{
    return [
        "data" => $secure,
        "authorization" => $permission
    ];
}
```

---

If you want to protect controller function accessed from not-authenticated user. 
You can seal-it with the auth doc command like below.

```php
/**
 * #Auth session true
 */
public function create() {}
```