---
title: XML Serializer
excerpt: Serialize and deserialize middleware that handles request and response data formatted as XML
---

## XML Serializer
The XML Serializer package contains two middleware, one for serialization and one for deserialization. The two works the same the only difference is that the serializer takes an array and returns XML and the deserializer does the opposite.

The serializer reacts if the <code>Accept</code> header matches one of the supported mime types and the deserializer reacts if the <code>Content-Type</code> matches the list of supported mime types.

By default the supported mime types are: <code>application/xml</code>. It is possible to add more mime types by passing an array to the constructor.


### Installation
This middleware is **not** included by default in the [Phapi Framework](https://github.com/phapi/phapi-framework) but if you need to install it it's available to install via [Packagist](https://packagist.org) and [Composer](https://getcomposer.org).

```bash
$ php composer.phar require phapi/serializer-xml:1.*
```

### Configuration
Both the serializer and deserializer has one configuration option, it's possible to add more mime types that should trigger the serializer/deserializer.

```php
<?php
use Phapi\Middleware\Serializer\Xml\Xml;

$pipeline->pipe(new Xml(['text/html']));
```

Note that the array passed to the constructor will be merged with the default settings.

The above instructions applies to the deserializer as well.

See the [configuration documentation](http://phapi.github.io/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.
