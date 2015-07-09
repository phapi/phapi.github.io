---
title: Implementing Cache Providers
excerpt: Learn how to implement the Cache Contract and how to handle problems while connecting to the cache backend
---

## Implementing cache providers
Implementing a new cache package connecting to a cache backend is really easy. There are two important things to know how to implement: the [Cache Contract](https://github.com/phapi/contract/blob/master/src/Phapi/Contract/Cache/Cache.php) and connecting to the cache backend.

## The Cache Contract
Implementing the Cache Contract is just a matter of implementing five methods:

- <code>set($key, $value)</code> - Save the key and value to the cache backend
- <code>get($key)</code> - Get the value for the key from the cache backend
- <code>has($key)</code> - Check if key exists (return boolean)
- <code>clear($key)</code> - Remove the key from the cache
- <code>flush()</code> - Clear the cache

```php
<?php

namespace Phapi\Contract\Cache;

/**
 * Cache
 *
 * If we are unable to connect to the cache backend an Exception should be
 * thrown. That Exception should be handled by the method calling this connect
 * method.
 *
 * A working cache is NOT a requirement for the application to run so it's
 * important to handle the exception and let the application keep running.
 * Suggestion: if the exception below is thrown a new NullCache should be created
 *
 * @category Phapi
 * @package  Phapi\Contract
 * @author   Peter Ahinko <peter@ahinko.se>
 * @license  MIT (http://opensource.org/licenses/MIT)
 * @link     https://github.com/phapi/contract
 */
interface Cache {

    /**
     * Set/add something to the cache
     *
     * @param  string $key Key for the value
     * @param  mixed  $value Value
     */
    public function set($key, $value);

    /**
     * Get something from the cache
     *
     * @param  string $key Key for the value
     * @return mixed
     */
    public function get($key);

    /**
     * Remove something from the cache
     *
     * @param  string $key Key for the value
     */
    public function clear($key);

    /**
     * Check if cache has a value for the key
     *
     * @param  string $key Key for the value
     */
    public function has($key);

    /**
     * Flush cache
     */
    public function flush();

}
```

## Connect to the backend

> Phapi has one important rule regarding cache: A working cache should not be a requirement for the application to work. So if Phapi is unable to connect to the cache backend it wont stop the execution. Instead the configured cache will be replaced with a dummy cache, new NullCache().

To achieve this the <code>construct()</code> method should try and connect to the cache backend. If that fails it should handle any **errors** that the backend or PHP throws and instead throw an Exception. This exception will be handled by Phapi and an instance of the [NullCache](https://github.com/phapi/cache-nullcache) will be used instead so that the execution of the application can continue.
