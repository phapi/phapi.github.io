---
title: JSONP Serializer
excerpt: Serializer middleware that handles response data formatted as JSONP
---

# JSONP Serializer

The JSONP Serializer package contains only one middleware, for serialization. The JSONP serializer works perfectly with the [JSON deserializer](/docs/serializer/json/).

The serializer reacts if the <code>Accept</code> header matches one of the supported mime types.

By default the supported mime types are: <code>application/javascript</code> and <code>text/javascript</code>. It is possible to add more mime types by passing an array to the constructor.

## Installation
This middleware is **not** included by default in the [Phapi Framework](https://github.com/phapi/phapi-framework) but if you need to install it it's available to install via [Packagist](https://packagist.org) and [Composer](https://getcomposer.org).

```shell
$ php composer.phar require phapi/serializer-jsonp:1.*
```

## Configuration
The serializer has two configuration options:
- The name of the request header that contains the callback function name. *The default header name is set to **X-Callback***:
- Additional mime/types that the serializer should support.

```php
<?php
use Phapi\Middleware\Serializer\Jsonp\Jsonp;

$pipeline->pipe(new Xml($callbackHeader = 'X-Callback', ['text/html']));
```

Note that the array with additional mime types passed to the constructor will be merged with the default settings.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.

## Callback header
Please note that if the defined callback header cant be found or isn't a valid function name the serializer will serialize the response as JSON without including the provided callback function name.

## HTTP Status code
The HTTP status code is included in the body if an error occurs and the HTTP status is changed to 200 since many/all clients will have problems handling a response with a HTTP status that isn't 200.

You can read more about the problem with JSONP and HTTP status codes [here](http://www.theguardian.com/info/developer-blog/2012/jul/16/http-status-codes-jsonp).
