---
title: JSON Serializer
excerpt: Serialize and deserialize middleware that handles request and response data formatted as JSON
---

## JSON Serializer
The JSON Serializer package contains two middleware, one for serialization and one for deserialization. The two works the same the only difference is that the serializer takes an array and returns JSON and the deserializer does the opposite.

The serializer reacts if the <code>Accept</code> header matches one of the supported mime types and the deserializer reacts if the <code>Content-Type</code> matches the list of supported mime types.

By default the supported mime types are: <code>application/json</code> and <code>text/json</code>. It is possible to add more mime types by passing an array to the constructor.

## Configuration
Both the serializer and deserializer has one configuration option, it's possible to add more mime types that should trigger the serializer/deserializer.

```php
<?php
use Phapi\Middleware\Serializer\Json\Json;

$pipeline->pipe(new Json(['text/html']));
```

Note that the array passed to the constructor will be merged with the default settings.

The above instructions applies to the deserializer as well.
