---
title: Cache providers
excerpt: Learn more about how Cache providers can be used and why they exists
---

## Introduction to cache providers
Cache providers are an adapter that communicates with a backend cache provider. The adapter can save, receive and delete data from the backend cache.

## How are they used
Cache providers are used through out the Phapi framework. It's for example used to store routes to speed up the routing process. It can also be used by [middleware](/docs/middleware/introduction/) as well as [endpoints](/docs/core/endpoints/) to store and receive data that needs to be persistent between requests.

```php
<?php
// Retrieve the cache provider
$cache = $this->container['cache'];

// Add something to the cache
$cache->set('test', 'value');

// Read something from the cache
echo $cache->get('test'); // Will echo "value"

// Check if something exists in the cache
$bool = $cache->has('test');

// Remove from cache
$cache->clear('test');

// Flush the cache
$cache->flush();
```

## How to implement your own
See the [implement your own cache provider](/docs/implement/cache/) section for more information.

## Existing cache providers
The list of cache providers are currently quite slim but more providers will be added later on.

Phapi does not include any Cache Providers by default.

### Extra
- [Memcache](/docs/cache/memcache/)
- [Redis](/docs/cache/redis/)

### Third party
There are currently no third party cache providers. [Get in contact](/contact/) if you have implemented one and want it listed here.
