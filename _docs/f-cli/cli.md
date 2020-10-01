---
title: CLI
category: Puko Console
order: 1
---

Puko framework shipped out with CLI named **Puko Console** as dev-dependency helper tools when we developing website.
You can see what Puko Console can do with help command:

```text
php puko help
```

List of available command you can use:

```text
setup    Installation
         [db]
         [secure]
         [auth] [name]
         [controller] [view/service] [name]
         [model] [add/update/remove] [name] [schema]
         
routes   Routing
         [view/service/console/list/error/lost] [add/update/delete/crud] [url]

generate Auto generate service
         [db]

serve    Start project on localhost
         [port]
         
tests    Start unit testing (preview)

element  Generate or download view element (beta)
         <name> [add/download]
         
cli      Execute code directly from console
         <router path>
         
help     Show help menu

version  Show console version
```

