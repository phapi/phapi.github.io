---
title: Middleware
excerpt: The pipeline of your application
---

## Uuid
The Phapi UUID Middleware generates an UUID (version 4) and adds it to the request object (as an attribute) and as a header to the response object. This makes it easier to debug problems as the client can refer to an UUID when contacting the API provider for help. If the UUID is used while logging it's easier for the provider to find the important information in the logs.

## Configuration
No configuration is needed since the middleware does not have any configuration options and it's enabled by default.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.

## Usage

```php
<?php
// Get the attribute from the request
$uuid = $request->getAttribute('uuid', null);

// Get header from response
$uuid = $response->getHeaderLine('uuid');

```
