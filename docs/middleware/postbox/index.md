---
layout: docs
title: Middleware
excerpt:  The pipeline of your application
---

## Postbox
The Postbox middleware has one simple task; take the Content-Type header from the request and check if there is a Deserializer that supports the mime type. If the mime type isn't supported an <code>415 UnsupportedMediaType</code> exception will be thrown.

## Configuration
There is no configuration options available.

See the [configuration documentation](/docs/started/configuration/) for more information about how to configure the integration with the Phapi Framework.
