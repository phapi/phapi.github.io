---
title: Middleware
excerpt: The pipeline of your application
---

## Courier
Courier is a HTTP Middleware responsible for sending a response to the client. The middleware relies on PSR-7 compatible request and response objects.

## Configuration
No configuration is needed for this middleware.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.

## Usage
Populate the response object and Courier take care of sending the headers and body.
