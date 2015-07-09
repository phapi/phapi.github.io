---
title: Implementing middleware
excerpt: Learn how to implement PSR-7 compliant middleware
---

## Implementing middleware
Middleware requires a request and a response and a callback (<code>$next</code>) that is called if the middleware allows further middleware to process the request. If a middleware doesn't need or desire to allow further processing it should not call the callback (<code>$next</code>) and should instead return a response. Note that <code>$next</code> can be <code>null</code>.

The main task of a middleware is to process an incoming request and/or the response. The middleware must accept a request and a response (PSR-7 compliant) instance and do something with them.

The middleware must pass a request and a response to the ($next) callback and finally either return the response from the ($next) callback or by modifying the response before returning it.

**Examples:**

```php
<?php
  public function __invoke(
    Request $request,
    Response $response,
    callable $next)
  {
      // Do something ...

      return $next($request, $response, $next);
  }
```

**OR**

```php
<?php
  public function __invoke(
    Request $request,
    Response $response,
    callable $next)
  {
      // Do something ...

      $response = $next($request, $response, $next);

      // Modify response ...

      return $response;
  }
```

If the middleware should break the pipeline, example: the client hit the rate limit, it should return a response instead of invoking <code>$next</code>.

**Example:**

```php
<?php
  public function __invoke(
    Request $request,
    Response $response,
    callable $next)
  {
      if ($this->tooManyRequests()) {
        // Set appropriate headers and body

        // Return response
        return $response;
      }

      return $next($request, $response, $next);
  }
```

### Dependency Injection Container
If you implement a method named <code>setContainer()</code> the pipeline will call that method and provide the Dependency Injector Container that can be used in the <code>__invoke()</code> method.

**Example:**

```php
<?php
  public function setContainer($container)
  {
    $this->container = $container;
  }
```

### Complete example
Here is a complete example of how a middleware should look. Use this example as a starting point when you wan't to write your own middleware.

```php
<?php

namespace Phapi\Middleware\Example;

use Phapi\Contract\Di\Container;
use Phapi\Contract\Middleware\Middleware;
use Psr\Http\Message\ResponseInterface;
use Psr\Http\Message\ServerRequestInterface;

/**
 * Eample middleware
 *
 * @category Phapi
 * @package  Phapi\Middleware\Example
 * @author   Peter Ahinko <peter@ahinko.se>
 * @license  MIT (http://opensource.org/licenses/MIT)
 * @link     https://github.com/phapi/middleware-example
 */
class Example implements Middleware
{

    /**
     * Dependency injection container
     *
     * @var Container
     */
    private $container;

    /**
     * Set dependency injection container
     *
     * @param Container $container
     */
    public function setContainer(Container $container)
    {
        $this->container = $container;
    }

    /**
     * Invoking the middleware
     *
     * @param ServerRequestInterface $request
     * @param ResponseInterface $response
     * @param callable $next
     * @return ResponseInterface $response
     */
    public function __invoke(ServerRequestInterface $request, ResponseInterface $response, callable $next = null)
    {
        // Do something ...

        // Call next middleware
        $response = $next($request, $response, $next);

        // Do something with the response ...

        // Return the response
        return $response;
    }
}

```
