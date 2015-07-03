---
layout: docs
title: Middleware
excerpt: The pipeline of your application
---

## Content Negotiation
The Content Negotiation Middleware contains of one middleware designed to handle format negotiations. It takes the <code>Accept</code> header and parses it, matches it against the list of supported mime types (registered by serializers) and finally sets the proper <code>Content-Type</code> header on the response object.

## Configuration
No configuration is needed for this middleware.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.

## Usage
The format negotiation middleware sets the proper <code>Content-Type</code> header on the response object. The header value can be accessed by using the <code>getHeaderLine()</code> method:

```php
<?php
/*
 * Get the response content type header that has the negotiated header.
 *
 * Returns the header value including charset.
 * Example: application/json;charset=utf-8
 */
$mimeType = $response->getHeaderLine('Content-Type');
```

The middleware also sets the mime type and any parameters included in the accept header as attributes on the request object:


```php
<?php
// Get the negotiated mime type:
$mimeType = $request->getAttribute('Accept');

// Get parameters (as an array) included in the accept header
$acceptParameters = $request->getAttribute('Accept-Parameters');
```

## Exceptions
The middleware will throw a <code>406 NotAcceptable</code> if the requested mime type isn't supported. An <code>500 InternalServerError</code> is thrown if no serializers are found.

If the requested mime type isn't supported the first mime type in the first registered serializers will be used to serialize the error message sent to the client.
