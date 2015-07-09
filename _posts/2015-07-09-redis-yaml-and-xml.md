---
title: Redis, YAML & XML
tags:
  - cache
  - serializers
author:
  name: Peter Ahinko
---

In the last few days I've added two new serializers packages. This makes it really easy to add [YAML](/docs/serializers/yaml/) and [XML](/docs/serializers/xml/) support to your API. Besides the two serializers a [Redis Cache Provider](/docs/cache/redis/) package is also available. Redis is one of the fastest options available and it's rich features makes it a popular choice.

<!--more-->

## YAML & XML Serializers
The two serializers supports the usual <code>Content-Type</code> headers by default. The YAML serializer supports <code>application/x-yaml</code>, <code>text/x-yaml</code> and <code>text/yaml</code> while the XML Serializer supports <code>application/xml</code>.

Install the serializers by adding them as dependencies to your composer configuration:

```bash
$ php composer.phar require phapi/serializer-yaml:1.*
$ php composer.phar require phapi/serializer-xml:1.*
```

Last but not least: add the serializers to your configuration in the <code>app/configuration/middleware.php</code> file by adding them right after the JSON serializer:

```php
<?php

/*
 * Serializer middleware serializers the response body to the format that the client prefers
 */
$pipeline->pipe(new \Phapi\Middleware\Serializer\Json\Json());

/*
 * The following serializers are NOT installed by default. See the documentation for
 * more information about how to install them before uncommenting the line(s) below.
 */
$pipeline->pipe(new \Phapi\Middleware\Serializer\Yaml\Yaml());
$pipeline->pipe(new \Phapi\Middleware\Serializer\Xml\Xml());
```

The deserializers should be added right after the JSON deserializer:

```php
<?php

/*
 * Deserializer middleware that deserializes any content provided in the request.
 */
$pipeline->pipe(new \Phapi\Middleware\Deserializer\Json\Json());

/*
 * The following serializers are NOT installed by default. See the documentation for
 * more information about how to install them before uncommenting the line(s) below.
 */
$pipeline->pipe(new \Phapi\Middleware\Deserializer\Yaml\Yaml());
$pipeline->pipe(new \Phapi\Middleware\Deserializer\Xml\Xml());

```

## Redis Cache Provider
The new Redis Cache Provider requires a working installation of [Redis](http://redis.io).

Install the provider by adding them as dependencies to your composer configuration:

```bash
$ php composer.phar require phapi/cache-redis:1.*
```

The configuration is easy to set up, edit the <code>app/configuration/settings.php</code> file and make sure these lines are uncommented:

```php
<?php

/*
 * Redis example. Please note that the Redis Cache Provider is NOT included by default by
 * Phapi. Please see https://github.com/phapi/cache-redis for more information about how to
 * install the package. When the package is installed, uncomment and modify host and port
 * (if needed). Please note that this version of the Redis Cache Provider does NOT support
 * redis clusters.
 */
$container['cache'] = function ($container) {
    return new \Phapi\Cache\Redis\Redis($servers = [
        [
            'host' => 'localhost',
            'port' => 6379,
        ]
    ]);
};

```
