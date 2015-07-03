---
layout: docs
title: Routes
excerpt: Learn how to set up routes to your endpoints
---

## Introduction
By default the Phapi Framework comes with a [Route middleware](/docs/middleware/route/) that handles the routing process. To keep Phapi simple and easy to use it was designed to only support one type of routing. A route will always lead to an Endpoint. You can not use closures. Due to how [Endpoints](/docs/core/endpoints/) are designed there is no need to involve HTTP Verbs when defining routes. The router will handle that automatically by looking at the request method and the defined methods in the endpoint.

## Defining routes
Routes are defined by creating an array with the route as the key and the name of the endpoint (including namespace) as the value.

```php
<?php

// Create a list of routes
$routes = [
  '/users'                  => '\\Phapi\\Endpoint\\Users',
  '/users/{name:a}'         => '\\Phapi\\Endpoint\\User',
  '/articles/{id:[0-9]+}'   => '\\Phapi\\Endpoint\\Article',
  '/blog/{slug}/{title:c}?' => '\\Phapi\\Endpoint\\Blog\\Post',
];
```

By default a route pattern syntax is used where **{foo}** specified a placeholder with name **foo** and matching the string **[^/]+**. To adjust the pattern the placeholder matches, you can specify a custom pattern by writing **{bar:[0-9]+}**.

To make a placeholder optional, use a question mark **?**. See the fourth line in the example above. The **{title:c}** is optional.

#### Regex Shortcuts
```php
:i => :/d+                # numbers only
:a => :[a-zA-Z0-9]+       # alphanumeric
:c => :[a-zA-Z0-9+_-\.]+  # alnumnumeric and +-_. characters
:h => :[a-fA-F0-9]+       # hex
```
