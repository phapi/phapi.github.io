---
title: Middleware
excerpt: The pipeline of your application
---

# Rate Limit Middleware

The rate limit middleware handles how many times a client are allowed to do requests to endpoints. Different settings can be set to different endpoints so it is possible that a client are allowed to do more requests to one endpoint than another endpoint. **Please note** that, depending on the configuration, this middleware uses different counters for each endpoint and client. So if a client hits the limit on one endpoint might not stop the client from doing request to other endpoints.

## Installation
This middleware is **not** included by default in the [Phapi Framework](https://github.com/phapi/phapi-framework) but if you need to install it it's available to install via [Packagist](https://packagist.org) and [Composer](https://getcomposer.org).

```bash
$ php composer.phar require phapi/middleware-rate-limit:1.*
```

## Configuration
There are a few settings that needs to be configured before the rate limit middleware works.

**The rate limit middleware requires a cache, for example Memcache**.

The middleware constructor needs four parameters, the name of the header that should be used as the identifier for each client, rate limit buckets, cache and the name of the request attribute that the route middleware used to store the matched endpoint.

The unique identifier can for example be a <code>Client-ID</code> or something else that is used for identification. This is usually the same header that's used for authentication.

The rate limit buckets are essentially settings on a endpoint level. The <code>\Phapi\Middleware\RateLimit\Bucket()</code> constructor takes four parameters:

* Total number of tokens in bucket (default: **800**),
* Number of new tokens that should be added within a time window (default: **400**),
* Time window in number of seconds (default: **60**),
* If new tokens should be added continuously (true) or if the time window needs to pass (false) before new tokens are added (default: **true**).

A default bucket is required. This bucket will act as a fallback if the requested endpoint does not have an own bucket. Example:

```php
<?php
// config rate limit middleware resources
$rateLimitBuckets = [
    'default' => new \Phapi\Middleware\RateLimit\Bucket(),
    '\\Phapi\\Endpoint\\Page' => new \Phapi\Middleware\RateLimit\Bucket(600, 60, 10, false),
];
// Add Middleware
$pipeline->pipe(new \Phapi\Middleware\RateLimit(
  'Client-ID',
  $rateLimitBuckets,
  $container['cache'], // Get the configured cache
  $requestAttribName = 'routeEndpoint' // The name of the attribute that the route middleware used to store the matched endpoint.
));
```

The <code>$requestAttribName</code> doesn't need to be used if you use the [route middleware](/docs/middleware/route/) and you use it's default configuration.

## Exceptions
The middleware throws <code>\Phapi\Exception\InternalServerError</code> when:
- no default bucket is configured
- when it's unable to find the matched endpoint (check $requestAttribName)
- no cache is configured

It also throws <code>\Phapi\Exception\TooManyRequests</code> when the counter hits zero and the client has run out of tokens.
