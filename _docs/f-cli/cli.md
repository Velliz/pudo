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

* Setup 

If you want to see about `setup db` or `setup secure` you can refer to **Configuration** page.

Jump to another setup, there is `setup auth`. You can also refer to **Authentication** page.

* Routes

If you want to see information about `routes view`, you can refer to **View** page.

If you want to see information about `routes service`, you can refer to **Service** page.

* Generate

`php puko generate db` command will create the database based on model schema in `plugins\model`

* Serve

You can run *Puko* without using a web server. Use *command* below to run it directly:

```text
php puko serve [POST_NUMBER]
```

* Tests

> TODOCS

* Element

> TODOCS

* Cli

`php puko cli [ROUTE_URL]` will execute controllers directly from php.

* Help

Show all available commands.

* Version

Most simple command is check the cli version: `php puko version`
