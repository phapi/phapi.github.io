---
layout: docs
title: Middleware
excerpt:  The pipeline of your application
---

## Mistake
The Mistake Middleware handles errors and exceptions by registering custom shutdown function, error handler and exception handler. When an error or exception is caught the middleware creates a log entry and prepares an error message that will be sent to the client before interacting with the pipeline by reseting the queue and telling the pipeline to only call middleware registered before the Mistake Middleware (usually only serializers and middleware responsible for sending the response to the client).

## Configuration
There is one configuration option available for the Mistake Middleware; if error messages should be shown. This is handy to have enabled during development since it gives a more detailed error message. It should however **be turned off in production** since an error message will be serialized and return to the client. (Default: off).

```php
<?php

// For development
$pipeline->pipe(new \Phapi\Middleware\Mistake\Mistake($displayErrors = false));
```

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.
