---
layout: docs
title: Middleware
excerpt:  The pipeline of your application
---

## Method Override
Middleware handling and allowing to override the original request method. This is useful when the client aren't able to send other native request methods than GET and POST.

## Configuration
It's possible to configure what override methods are allowed when the original request method is GET or POST.

Default settings:

* <code>'CONNECT', 'TRACE', 'HEAD', 'OPTIONS'</code> are allowed to override <code>GET</code> requests.
* <code>'PATCH', 'PUT', 'DELETE', 'COPY', 'LOCK', 'UNLOCK'</code> are allowed to override <code>POST</code> requests.

A 405 Method Not Allowed will be returned to the client if the override method aren't allowed due to the original request method (for example: override GET with PUT).

```php
<?php

$pipeline->pipe(new \Phapi\Middleware\Override\Method(
  // Replace allowed methods to override GET
  ['HEAD', 'OPTIONS'],
  // Replace allowed methods to override POST
  ['PUT', 'DELETE']
);

```

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.
