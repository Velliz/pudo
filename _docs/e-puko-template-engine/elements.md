---
title: Elements
category: Puko Template Engine
order: 2
---

Element is a *feature set* originally from pte, 
template engine that is puko framework used to create segments of view as standalone modular modules, detachable, and reusable.
The element itself consists of a package of html, javascript, css and php file to manage the logic of these elements.

To download the Element set, you can use the following *command*.
 
```text
php puko element download adminlte_description
```

Note: you can see what elements are available for download from [this](https://github.com/Velliz/elements) page.

You can also create a new element with the command:

```text
php puko element add <element_name>
```

You can change <element_name> name it freely according to your wishes.

> Attention: naming elements must not use spaces or numbers in front of them. Recomends to include [a-z_A-Z] character only.

After an element is created or downloaded, it will be saved in the directory like the structure shown below.

```text
- plugins
  - elements
   - <element_name>
     - <element_name>.php
     - <element_name>.html
     - <element_name>.js
     - <element_name>.css
```

For experiments, you can start from downloading the following sample first:

```text
php puko element download adminlte_description
```

Then create the Element instance from the controller.

```php
public function profile() 
{
    //call element PHP class
    $desc = new AdminLTE_Description('desc', array());
    $desc->SetStyle(AdminLTE_Description::HORIZONTAL);
    $desc->SetDescription(array(
        array(
            'Title' => 'Didit Velliz',
            'Text' => 'Programmer',
        ),
        array(
            'Title' => 'Lois',
            'Text' => 'Gamer',
        ),
        array(
            'Title' => 'Christian',
            'Text' => 'Lead Developer',
        )
    ));
    $data['desc'] = $desc;
}
```

On the html page, you can render the tag by writing:

```html
<div>
    {!desc}
</div>
```
