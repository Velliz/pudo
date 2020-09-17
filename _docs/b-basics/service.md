---
title: Service
category: Basics
order: 5
---

Use service to create web-service. Because puko directly return the data in json format.
You can instantly scaffolds your service with `php puko routes serice add ...`.
Querying data and return it at the end of controller functions. 
The noticeable thing you can find is in controller at the extends section.

```php
class students extends Service {}
```
You're right! The controller file is simply extends `Service` to create web-service instead `View` that processing html file.

For example, if we have the controller showed bellow:

```php
public function students() {

    //app logic in here
    //database operation maybe in here to

    return [
        'Identification' => 'ID120027103',
        'Name' => 'Didit Velliz',
        'Age' => 26,
        'Skills' => [
            'PHP', 'MySQL'
        ]
    ];
}
```

So the json representational of the data returned from controller is:

```json
{
    "Identification": "ID120027103",
    "Name": "Didit Velliz",
    "Age": 16,
    "Skills": [
      "PHP",
      "MySQL"
    ]
}
```

Passing dynamic data retrieved from url parameter is also possible with `{?}` keywords when create new route.
