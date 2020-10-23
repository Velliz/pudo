---
title: Console
category: Basics
order: 8
---

Sometimes, when coding. We not always relay on web server like **apache** or **nginx**.
Maybe we need code executed outside the web server world. So to achieve this needs, 
Puko come with feature called `Console`. So what is the benefit of this?

* Secure

Because `console` don't rely on web server. You don't communicate anymore with http protocol.
Your process running inside server and secure by default.

* No timeout

Say goodbye to request timeout raised by web server. 
Now you can run very heavy script and running for all day long. No problem!

* Event-driven

Move out from PHP blocking I/O behavior. With `console` now you can enter the reactive world of PHP.

* Message Queue Consumer

Listen into messages broadcased by message-broker server now possible.

* WebSocket Server

Write a websocket server with `console`.

And many another possibilities that default PHP cannot provide.

---

Working with `console` is easy as working with `view` or `service` controller. 
The noticeable thing you can find is in controllers at the extends section.

```php
class students extends Console {}
```

You can also generate it with puko console `php puko routes console add <route_name>` 
but all console route will set for default to accept GET verb. for example:

```text
php puko routes console add message/forgot/password/subscribe

controller name: console\forgot\password
method: subscribe
```

You can place code same as the regular controller.

Then run your script from cli/powershell/terminal:

```
php cli message/forgot/password/subscribe <arguments>
```

> For now puko framework allow only 1 argument