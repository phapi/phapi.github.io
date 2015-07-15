---
title: CORS & Rate Limiting
permalink: /blog/cors-and-rate-limiting
tags:
  - middleware
  - cors
  - rate limit
author:
  name: Peter Ahinko
---

The latest additions to the middleware stack is a middleware for handling HTTP Access Control (CORS) requests as well as a middleware for setting up rate limits on either the entire api or specific endpoints, or a combination of the two.

<!--more-->

## CORS
HTTP Access Control (CORS) can be difficult to both understand and handle. So what is CORS?

> Cross-site HTTP requests are HTTP requests for resources from a different domain than the domain of the resource making the request. For instance, a resource loaded from Domain A (http://domaina.example) such as an HTML web page, makes a request for a resource on Domain B (http://domainb.foo), such as an image, using the img element (http://domainb.foo/image.jpg). This occurs very commonly on the web today — pages load a number of resources in a cross-site manner, including CSS stylesheets, images and scripts, and other resources.

> Cross-site HTTP requests initiated from within scripts have been subject to well-known restrictions, for well-understood security reasons. For example HTTP Requests made using the XMLHttpRequest object were subject to the same-origin policy. In particular, this meant that a web application using XMLHttpRequest could only make HTTP requests to the domain it was loaded from, and not to other domains. Developers expressed the desire to safely evolve capabilities such as XMLHttpRequest to make cross-site requests, for better, safer mash-ups within web applications.

Source: [https://developer.mozilla.org/en-US/docs/Web/HTTP/AccesscontrolCORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/AccesscontrolCORS)

The CORS middleware is designed to handle this for you. The configuration allows us to specify a variety of rules that applies to all requests that include a <code>origin</code> header. If no such header is included the request is not considered to be a cross-site request.

See the [documentation](http://phapi.github.io/docs/middleware/cors/) for more information about the CORS middleware.

## Rate limit
The rate limit middleware can be configured in different ways. You can either add one rule that applies to the entire API. For example a client might be allowed to do 800 requests during a 1 hour window. Or you might want to have additional rules for specific endpoints. The middleware has two different requirements. A cache must be configured, and the clients must send a specific header with some kind of identifier. You can specify the header name and a suggestion is to use the same header that's used for authentication and authorization.

See the [documentation](http://phapi.github.io/docs/middleware/rate-limit/) for more information about the Rate limit middleware.
