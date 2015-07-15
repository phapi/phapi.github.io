---
title: Middleware
excerpt: The pipeline of your application
---

# HTTP Access Control (CORS)
> Cross-site HTTP requests are HTTP requests for resources from a different domain than the domain of the resource making the request.  For instance, a resource loaded from Domain A (http://domaina.example) such as an HTML web page, makes a request for a resource on Domain B (http://domainb.foo), such as an image, using the img element (http://domainb.foo/image.jpg).  This occurs very commonly on the web today — pages load a number of resources in a cross-site manner, including CSS stylesheets, images and scripts, and other resources.

> Cross-site HTTP requests initiated from within scripts have been subject to well-known restrictions, for well-understood security reasons.  For example HTTP Requests made using the XMLHttpRequest object were subject to the same-origin policy. In particular, this meant that a web application using XMLHttpRequest could only make HTTP requests to the domain it was loaded from, and not to other domains.  Developers expressed the desire to safely evolve capabilities such as XMLHttpRequest to make cross-site requests, for better, safer mash-ups within web applications.

Source: [https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)

The CORS middleware handles these requests for the application.

## Installation
This middleware is **not** included by default in the [Phapi Framework](https://github.com/phapi/phapi-framework) but if you need to install it it's available to install via [Packagist](https://packagist.org) and [Composer](https://getcomposer.org).

```bash
$ php composer.phar require phapi/middleware-cors:1.*
```

## Configuration
The CORS Middleware has a few configuration options. In it's simplest form it can be configured like this:

```php
<?php
$corsOptions = [
    'allowedOrigins' => ['*'],
    'allowedMethods' => ['*'],
    'allowedHeaders' => ['*'],
    'exposedHeaders' => [],
    'maxAge' => 3600,
    'supportsCredentials' => false,
];
$pipeline->pipe(new \Phapi\Middleware\Cors($corsOptions));
```

### Explanation
- **allowedOrigins** specifies the different origins that are allowed to make CORS requests to the API. "*" means that there is no restrictions. Add each origin as a separate value in the array: ['http://foo.bar', 'http://domain.example']

- **allowedMethods** is a list of methods that are allowed. Example: ['GET', 'POST', 'OPTIONS']

- **allowedHeaders** specifies headers that the client are allowed to send during a CORS request. Example: ['Client-ID', 'X-Modified']. Please note that some default headers are allowed, see the [Mozilla Developer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS) page for more information.

- **exposedHeaders** is a list of headers that the browser are allowed to expose for the user/script. Example ['X-Rate-Limit-Remaining']

- **maxAge** specifies how long (in seconds) the client can cache this information.

- **supportsCredentials** specifies if the API allows/supports credentials in a CORS request.

See the [configuration documentation](http://phapi.github.io/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.

## Exceptions
A <code>BadRequest</code> exception is thrown when either the **origin**, **method** or the <code>Access-Control-Request-Method</code> header is required but missing.
