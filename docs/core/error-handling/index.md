---
layout: docs
title: Error handling
excerpt: Some times we make mistakes, but how do we handle them?
---
## Introduction
In it's default configuration, Phapi comes with an [error handler in a form of a middleware](/docs/middleware/mistake/). This middleware is designed to catch any uncaught exceptions as well as errors. The middleware will generate an error message and then force the middleware pipeline to reset so that only the serializers and the middleware responsible for delivering the response to the client are invoked.

The core concept regarding error handling is to throw exceptions and let the error handler take care of the response to the client as well as creating log entries. *See the [configuration](/docs/started/configuration/) section for more information about how to set up logging.*

## Exceptions
Phapi comes with predefined [exceptions](https://github.com/phapi/exception). These exceptions represents different response codes that should be used to make the API more restful.

If none of the predefined exceptions fits the use case the recommendation is to throw an <code>\Phapi\Exception\InternalServerError</code> that will result in a 500 status code.

Each of these exception includes a predefined <code>$statusCode</code>, <code>$statusMessage</code> as well as a <code>$description</code>. Each of these can be overwritten but it's not recommended to replace the <code>$statusCode</code> nor <code>$statusMessage</code>. There is also a possibility to add a link to the response sent to the client that should point to some kind of documentation of the problem so that the user knows what the problem is. This can be done in two ways, either specify the link while throwing the exception:

```php
<?php
$link = 'http://somedomain.local/docs/errors/404';

throw new \Phapi\Exception\NotFound(null, null, null, null, $link);
```

This might not be convenient so another option is to extend the exception:

```php
<?php

namespace Example\Exception\NotFound;

class NotFound extends \Phapi\Exception\NotFound
{

  protected $link = 'http://somedomain.local/docs/errors/404';

}
```

And throw it:

```php
<?php
throw new \Example\Exception\NotFound();
```

### Included exceptions
- BadGateway
- BadRequest
- Conflict
- Forbidden
- Gone
- InternalServerError
- Locked
- MethodNotAllowed
- NotAcceptable
- NotFound
- NotImplemented
- PaymentRequired
- RequestEntityTooLarge
- RequestTimeout
- ServiceUnavailable
- TooManyRequests
- Unauthorized
- UnprocessableEntity
- UnsupportedMediaType
