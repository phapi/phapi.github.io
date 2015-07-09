---
layout: docs
title: Memcache
excerpt: Do you want to use Memcache as your cache backend? Well then you have come to the right place.
---

## Memcache
Memcache is a cache package using [Memcache](http://php.net/manual/en/book.memcache.php) as backend. Therefor [Memcache](http://php.net/manual/en/book.memcache.php) is required to be install for this package to work. However, Phapi has one golden rule regarding cache backends:

> A working cache should **not** be a requirement for the application to work. So if Phapi is unable to connect to the cache backend it wont stop the execution. Instead the configured cache will be replaced with a dummy cache, <code>new NullCache()</code>.

## Installation
The package is **not** installed by default by the Phapi framework. Add the package as a dependency in composer to install the package.

```shell
$ composer require phapi/cache-memcache:1.*
```

## Configuration
Configure the package and add it to the container to enable it.

```php
<?php
$container['cache'] = function ($container) {
    return new \Phapi\Cache\Memcache($servers = [
        [
            'host' => 'localhost',
            'port' => 11211
        ],
    ]);
};
```

Add as many memcache servers as you want by extending the array.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.
