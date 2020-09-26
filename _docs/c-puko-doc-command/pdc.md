---
title: Puko Doc Command
category: Puko Doc Command 
order: 1
---

Puko docs command build to simplify controller creation also for speed up backend development.
Implementation is quite simple. Just put the command above the class name or function name doc command.
For example:

```php
/**
 * #Master master-admin.html
 * #Value title Welcome
 * #Date before 31-08-2016 12:00:00
 */
 public class registrasi extends View {
```

Because the command placed like we adding comment in our code. 
Your code inside the function code itself is clean.
But, don't forget that command must identified with first hashtag # character.
Command always skipped by puko if the hashtag character not present.

```php
/**
 * #...
 */
```

This is complete catalog *command* available.

|*Command*|Key Identifier|Value|Function|
|---|---|---|---|
|#Value|name|Didit Velliz|To send data named **name** with value **Didit Velliz** directly to the view|
|#Template|master|true/false|Option to use master layout|
|#Template|html|true/false|Option to output html file in browser|
|#Template|cache|true/false|Option to cache output html with pte cache driver|
|#Date|before/after|d-m-Y H:i:s|Option for accessing **function**. So if the server time is outside the specified time then **function** cannot be accessed|
|#ClearOutput|binary|true/false|Option to output results processed through the framework|
|#Auth|bearer|true/false|Option for accessing functions. true to allow logged in only, false to allow all|
|#Auth|session|true/false|Option for accessing functions. true to allow logged in only, false to allow all|
|#Auth|cookies|true/false|Option for accessing functions. true to allow logged in only, false to allow all|
|#Master|-|master.html|Using a custom file for the master layout|
|#DisplayException|-|true/false|Forward the process to *View* or *Service* middleware when an exception occurs|
|#UnderConstruction|-|true/false|Display Under Construction page|
|#Permission|\pukoframework\auth\Bearer@\plugins\auth\UserAuth|permissions@MANAGER|Displaying an not have permission page if check fails|
