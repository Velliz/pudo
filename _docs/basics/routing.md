---
title: Routing
category: basics
order: 1
---

```php
<?php 
$data['page'] = array(
    '' => array(
        'controller' => 'main',
        'function' => 'main',
        'accept' => ['GET'],
    ),
    'profile' => array(
            'controller' => 'accounts\accounts',
            'function' => 'profile',
            'accept' => ['GET', 'POST'],
    )
);

$data['error'] = array(
    'controller' => 'main',
    'function' => 'error',
    'accept' => ['GET', 'POST', 'PUT', 'HEAD']
);

$data['not_found'] = array(
    'controller' => 'main',
    'function' => 'not_found',
    'accept' => ['GET', 'POST', 'PUT', 'HEAD']
);

return $data;
```