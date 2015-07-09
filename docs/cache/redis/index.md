---
title: Redis
excerpt: Do you want to use Redis as your cache backend? Well then you have come to the right place.
---

## Redis
Redis is a cache package using [Redis](http://redis.io) as backend. Therefor [Redis](http://redis.io) is required to be install for this package to work. However, Phapi has one golden rule regarding cache backends:

> A working cache should **not** be a requirement for the application to work. So if Phapi is unable to connect to the cache backend it wont stop the execution. Instead the configured cache will be replaced with a dummy cache, <code>new NullCache()</code>.

## Installation
The package is **not** installed by default by the Phapi framework. Add the package as a dependency in composer to install the package.

```shell
$ composer require phapi/cache-redis:1.*
```

## Configuration
Configure the package and add it to the container to enable it.

```php
<?php
$container['cache'] = function ($container) {
    return new \Phapi\Cache\Redis\Redis($servers = [
        [
            'host' => 'localhost',
            'port' => 6379,
        ]
    ]);
};
```
The Redis cache provider does currently **not** support clusters.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.
