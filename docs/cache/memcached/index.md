---
title: Memcached
excerpt: Do you want to use Memcache as your cache backend? Well then you have come to the right place.
---

## Memcached
Memcached is a cache package using [Memcached](http://php.net/manual/en/book.memcached.php) as backend. Therefor [Memcached](http://php.net/manual/en/book.memcached.php) is required to be install for this package to work. However, Phapi has one golden rule regarding cache backends:

> A working cache should **not** be a requirement for the application to work. So if Phapi is unable to connect to the cache backend it wont stop the execution. Instead the configured cache will be replaced with a dummy cache, <code>new NullCache()</code>.

## Memcache vs Memcached
Please note that there are two cache provider packages available: [phapi/cache-memcache](https://github.com/phapi/cache-memcache) and [phapi/cache-memcached](https://github.com/phapi/cache-memcached). The difference between the packages is the PHP extension they use.

### So which one should you use?
It depends on two things:

- Which extension do you have installed?
- PHP version. Both the [Memcache](http://php.net/manual/en/book.memcache.php) extension and the [Memcached](http://php.net/manual/en/book.memcached.php) exists for PHP 5.6 and HHVM. But according to the [gophp7 project extension catalog](https://github.com/gophp7/gophp7-ext/wiki/extensions-catalog) only Memcached will be updated to PHP 7.

## Installation
The package is **not** installed by default by the Phapi framework. Add the package as a dependency in composer to install the package.

```shell
$ composer require phapi/cache-memcached:1.*
```

## Configuration
Configure the package and add it to the container to enable it.

```php
<?php
$container['cache'] = function ($container) {
    return new \Phapi\Cache\Memcached($servers = [
        [
            'host' => 'localhost',
            'port' => 11211
        ],
    ]);
};
```

Add as many memcache servers as you want by extending the array.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.
