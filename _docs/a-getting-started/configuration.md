---
title: Configuration
category: Getting Started
order: 2
---

**Encryption**

Encryption required to secure many aspects in our applications. Puko framework mostly using this to secure
user authentication data in several forms. Sessions, Cookies, and Bearer. Puko can scaffolds this process with
`pukoconsole` tools included as dev-dependency.

> Puko using AES-256-CBC as encryption algorithms

To start configure Encryption, you can type in _console/terminal/powershell_:

```text
php puko setup secure
```

Items asked:

|Items|Description|Examples|
|---|---|---|
|Identifier|String text uniquely identify your app|inventory|
|Secure key|Strong text like passwords|s-inventoryApp2020#**|
|Cookies name|String text for cookie name|inventory|
|Session name|String text for cookie name|inventory|
|Session expired|Session expired number (in days) or blank for infinity|30|
|Session expired display text|Display text|Login to continue|
|Error display text|Display text|You don't have access to this application|

> You can also configure it manually from `config/encryption.php`