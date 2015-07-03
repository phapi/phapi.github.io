---
layout: docs
title: Installation
excerpt: What are the requirements and dependencies and how do you install Phapi?
---

## System requirements
- Web server with URL rewriting
- PHP 5.6 or newer

Phapi *might* work on earlier versions but it's not tested nor is it supported on earlier versions. Phapi is currently tested on PHP 5.6, PHP 7 and HHVM. The default configuration works on all three versions but there are individual extra packages that does not support all versions.

Here is a current list of packages with tests that does not pass on one or more versions:

- [phapi/cache-memcache](https://github.com/phapi/cache-memcache) -  Fails on PHP 7. This package is however **not** installed by default.

## Dependencies
There is one dependencies with the basic configuration.

- [phapi/http](https://github.com/phapi/http) extends [zendframework/zend-diactoros](https://github.com/zendframework/zend-diactoros).

There are however features and middleware that do have some dependencies. A list of these dependencies can be found here:

- [phapi/cache-memcache](https://github.com/phapi/cache-memcache) requires the [Memcache](http://php.net/manual/en/book.memcache.php) extension to be installed and working.


## PHP settings

It's suggested to turn off displaying of errors in production environments and rely on logging instead since Phapi has an error handler that will display serialized error messages.

During development it's beneficial however to display errors and setting error reporting to <code>E_ALL</code>.

## Install with configuration
The [phapi/phapi-configuration](https://github.com/phapi/phapi-configuration) project includes everything you need to set up a simple hello world example. **[Download the latest version](https://github.com/phapi/phapi-configuration/archive/master.zip)** of the package and extract it to an empty directory. This zip file includes all the default configuration. After you've extracted the zip file you need to run composer:

```bash
$ composer install
```

## Install with Composer
It is also possible to install Phapi by using [Composer](https://getcomposer.org/). Navigate to your project directory and execute the following bash command. This command will install the Phapi Framework and all dependencies into your project's <code>vendor/</code> directory. You will however have to manually handle the [configuration](/docs/started/configuration/).

```bash
$ composer require phapi/phapi
```

Next, require the Composer autoloader into your PHP script.

```php
<?php
require 'vendor/autoload.php';
```
