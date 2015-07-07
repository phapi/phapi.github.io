---
layout: docs
title: Configuration
excerpt: Learn how to configure your application
---

## Configuration
The [phapi/phapi-configuration](https://github.com/phapi/phapi-configuration) project includes everything you need to set up a simple hello world example. **[Download the latest version](https://github.com/phapi/phapi-configuration/archive/master.zip)** of the package and extract it to an empty directory if you haven't already done that. Or take a look at the files in the [repository](https://github.com/phapi/phapi-configuration).

## Default settings
The default settings file sets up the default <code>Request</code>, <code>Response</code>, <code>Log</code> and <code>Cache</code> as well as <code>Charset</code> and <code>HTTP version</code>.

## Overriding default settings
Use the <code>app/configuration/settings.php</code> file to override any of the default settings. You should **not** edit anything in the <code>app/configuration/default/</code> directory.

## Adding serializers and middleware
The order of adding (de)serializers and middleware to the middleware pipeline is important. But there is no general rule since all middleware are different. Serializers and deserializers should be added after each other so that's a little bit easier to set up.

**To help with this we've added a [suggested order](https://github.com/phapi/phapi-configuration/blob/master/app/configuration/middleware.php) in the [phapi/phapi-configuration](https://github.com/phapi/phapi-configuration/) project.**

## Logging
By default no logging is set up, instead a "dummy" logger is configured.

Lets set up [Monolog]() as the logger. First we need to add Monolog to composer:

```shell
$ composer require monolog/monolog
```

Next, open up <code>app/configuration/settings.php</code> and uncomment these lines:

```php
<?php
/*
 * Custom logging example. Please note that the Monolog package is NOT included by
 * default by Phapi. Please see the documentation for more information about how to
 * install the package. When the package is installed, uncomment the following lines
 * and modify them to match your needs.
 */
use Monolog\Logger;
use Monolog\Handler\StreamHandler;

$container['log'] = function ($container) {
    $log = new Logger('default');

    // IMPORTANT! Make sure you use an absolute path. Relative paths aren't guaranteed to
    // work in some cases where errors and exceptions occur.
    $log->pushHandler(new StreamHandler('/www/phapi/app/logs/logfile.log', Logger::WARNING));
    return $log;
};
```

## Cache
Phapi doesn't have a real cache configured by default. Instead a "dummy" cache is used.

Lets set up [memcached](http://www.memcached.org/) as our cache. First, install memcached and make sure the [PHP extension](http://php.net/manual/en/book.memcache.php) is installed as well.

Second, add [phapi/cache-memcache](https://github.com/phapi/cache-memcache) as a dependency.

```shell
$ composer require phapi/cache-memcache
```

Next, open up <code>app/configuration/settings.php</code> and uncomment these lines:

```php
<?php
/*
 * Memcache example. Please note that the Memcache package is NOT included by default
 * by Phapi. Please see https://github.com/phapi/cache-memcache for more information
 * about how to install the package. When the package is installed, uncomment and modify
 * host and port (if needed).
 */
$container['cache'] = function ($container) {
    return new \Phapi\Cache\Memcache($servers = [
        [
            'host' => 'localhost',
            'port' => 11211
        ]
    ]);
};
```
