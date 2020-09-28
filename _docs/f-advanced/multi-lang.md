---
title: Multi Language
category: Advanced
order: 2
---

Challenge faced when a website or api service dealing with multiple language is to maintain the overall performance.
To archive that expectations, multiple language in puko divided into 2 main concern: frontend and backend.
The very first step to determinate what language to use is client HTTP request. 
HTTP Request can vary from web browser, native mobile apps or desktop applications.

So when requesting resource to server, you can pass custom `X_LANG` 
header with value of 2 digits lowercase based country code as language code.
if the custom header don't exist puko will use default value 'id'.

In the code level, we can achieve it 2 step. First we will deal with frontend html file.
Separated html language is use to maintaining performance. With cost became redundant.

You can crate the html file like shown below:

```text
assets
   html
      en
         function
            template.html
      id
         function
            template.html
```

> you can add another language code by yourself like `cn`, `kr`, `jp` and so on.

---

In the backend side, language maintained directly from controller with function called `say()`.
For example:

```php
throw new Exception($this->say('NOT_FOUND'));
```

> say called with `$this` because the functions inherited from controller.

The 'NOT_FOUND' key you noticed is stored in json file in `assets/master/id.master.json` by default.
You can also add new json file with language code as you wish `en.master.json`, `cn.master.json' so on.

You can also pass a custom string into variable with second parameter of `say`

```php
throw new Exception($this->say('WRONG_ADDR', [$username, $email]));
```

Place %s in the json file to retreive the custom value:

```json
{
    "NOT_FOUND": "No data found",
    "WRONG_ADDR": "Address for %s not found with email: %s"
}
```

Now language resource can translated and centralized.
