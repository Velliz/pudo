---
title: Framework
category: Basics
order: 8
---

When writing code in controllers, you may sometimes wonder for a piece of code to generate random number, 
server date time, get site base url, get the base directory of your project in server and so on.

This section of page will list all the available helper method to address this needs. 
So you can use directly in controllers service/view/console.

* Get Server Date Time

`$this->GetServerDateTime()`

You can use that helper function to capture server date time in 'Y-m-d H:i:s'

* Generate Random Token

`$this-GetRandomToken()`

Function will produce random six length string contains [0-9a-zA-Z] for example: `p4vRXo`.
You can also customize the length smaller or greater than six with parameter.

`$this-GetRandomToken(16)`

The function above will produce sixteen length random string.

* App Constant

`$this->GetAppConstant('KEY')`

This function will get the constant defined in **config/app.php** in const section with name KEY.

* Redirect

`$this->RedirectTo('routing-path', false)`

The first param is the destination route param, and second param is boolean value when set to true
will replace the prev page. when set to false the redirection treated equivalent as click link.

* Say (Language)

`$this->say('LANGUAGE')`

Will fetch the correct language from json schema placed in assets/master. 
You can see further explanations in multiple language section.

* Base URL

`Framework::$factory->getBase()`

Retrieve web base url for example: http://localhost:3000/

* Root Path

`Framework::$factory->getRoot()`

Retrieve server path of code for example: /var/www/html/puko

* Get Environment

`Framework::$factory->getEnvironment()`

Retrieve environment info such as DEVELOPMENT or PROD.

* Get Start (PHP execution time)

`Framework::$factory->getStart()`

---

Override function also available to change the default behavior of the controller life cycles.
You can override 2 function:

```php
 public function BeforeInitialize()
{
    // you can take action before real function executed here
}

public function AfterInitialize()
{
    // you can take action after real function executed here
}
```
