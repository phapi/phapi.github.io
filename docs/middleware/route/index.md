---
layout: docs
title: Middleware
excerpt:  The pipeline of your application
---

## Route
The Route Middleware package contains two middleware: <code>Phapi\Middleware\Route\Route</code> and <code>Phapi\Middleware\Route\Dispatch</code> that handles routing and dispatch to [endpoints](/docs/core/endpoints/).

The Route Middleware will invoke the first route that matches the current HTTP request’s URI and method. If the request URI doesn't match any defined route a **404 Not Found** will be returned to the client. If the request method isn't implemented a **405 Method Not Allowed** will be returned instead.

The router does three things to be able to find a match, first it tries to find a direct match. This is possible for routes that doesn't contain regular expressions. If no direct match can be found the router will look in it's cache for a match. As a last resort the router tries to match against the routes that contains regular expressions. If a match is found it will be added to the cache.

## Configuration
The configuration contains three steps:

- Create middleware objects
- Define routes
- Add to pipeline

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.

### Create objects

```php
<?php

use Phapi\Middleware\Route\Route;
use Phapi\Middleware\Route\Router;
use Phapi\Middleware\Route\RouteParser;
use Phapi\Middleware\Route\Dispatch;

// Use the dependency injection container to get the configured cache
$route = new Route(new Router(new RouteParser, $container['cache']));
```

### Define routes
Routes can be added by passing an array (with the route as the key and the name of the endpoint as the value) to the **addRoutes** function.

```php
<?php

// Create a list of routes
$routes = [
  '/users'                  => '\\Phapi\\Endpoint\\Users',
  '/users/{name:a}'         => '\\Phapi\\Endpoint\\User',
  '/articles/{id:[0-9]+}'   => '\\Phapi\\Endpoint\\Article',
  '/blog/{slug}/{title:c}?' => '\\Phapi\\Endpoint\\Blog\\Post',
];

$route->addRoutes($routes);
```

By default a route pattern syntax is used where **{foo}** specified a placeholder with name **foo** and matching the string **[^/]+**. To adjust the pattern the placeholder matches, you can specify a custom pattern by writing **{bar:[0-9]+}**.

#### Regex Shortcuts
```php
:i => :/d+                # numbers only
:a => :[a-zA-Z0-9]+       # alphanumeric
:c => :[a-zA-Z0-9+_-\.]+  # alnumnumeric and +-_. characters
:h => :[a-fA-F0-9]+       # hex
```

### Add to pipeline
Last but not least, add the middleware to the pipeline. The <code>Dispatcher</code> doesn't need any configuration.

```php
<?php
$pipeline->pipe($route);
$pipeline->pipe(new \Phapi\Middleware\Route\Dispatcher());

```

### Complete example

```php
<?php

use Phapi\Middleware\Route\Route;
use Phapi\Middleware\Route\Router;
use Phapi\Middleware\Route\RouteParser;
use Phapi\Middleware\Route\Dispatch;

// Use the dependency injection container to get the configured cache
$route = new Route(new Router(new RouteParser, $container['cache']));

// Create a list of routes
$routes = [
  '/users'                  => '\\Phapi\\Endpoint\\Users',
  '/users/{name:a}'         => '\\Phapi\\Endpoint\\User',
  '/articles/{id:[0-9]+}'   => '\\Phapi\\Endpoint\\Article',
  '/blog/{slug}/{title:c}?' => '\\Phapi\\Endpoint\\Blog\\Post',
];

$route->addRoutes($routes);

$pipeline->pipe($route);
$pipeline->pipe(new \Phapi\Middleware\Route\Dispatcher());
```
