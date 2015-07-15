---
title: Middleware
excerpt: What is middleware and how does it work?
---

## Introduction to middleware
The basic concept of middleware can be summed up in a single method signature:

```php
function ($request, $response, $next)
```

The concept is easy to understand, we have a <code>$request</code> and a <code>$response</code> that we can do something with and we have the <code>$next</code> middleware that we can call whenever we need and want to. <code>$next</code> can either be an object or a callable.

Many other frameworks adds middleware as concentric layers surrounding the core application. Phapi however doesn't have a core application since almost every feature and all functionality is implemented as a middleware. The drawback of this approach is that you really have to think about the order of which the middleware is added to the pipeline.

The benefits with middleware are many:

- It's **easy to understand** and write your own middleware.
- It's **easy to add** new features and new functionality when needed since you only need to add it to the pipeline.
- **Reusable**, use middleware written for other frameworks and solutions as long as they have the same method signature.
- **Performance**, the whole application doesn't have to be executed if an early middleware can return the proper response.

When you run the application the Request and Response objects traverse the middleware structure from the outside in. They first enter the outer-most middleware, then the next outer-most middleware, (and so on). When the last middleware has been invoked the pipeline traverses the middleware structure from the inside out. Ultimately, a final response object exits the outer-most middleware.

A middleware anywhere in the pipeline can halt the traversing from the outside in and begin traverse back from the inside out. This is for example done when the client isn't allowed to do access the requested endpoint etcetera.

## How are they used
Phapi uses middleware to almost all functionality and features. Middleware are used to handle routing and dispatching as well as content negotiation. Even the serializers and all the error handling are middleware handling those tasks.

## How to implement your own
See the [implement your own middleware](/docs/implement/middleware/) section for more information.

## Existing middleware
Since Phapi relies heavily on middleware the list of available middleware is extensive and more middleware are added on a regular basis.

### Included by default
Phapi includes these middleware by default:

- [Content Negotiation](/docs/middleware/content-negotiation/)
- [Courier](/docs/middleware/courier/)
- [Method Override](/docs/middleware/method-override)
- [Mistake](/docs/middleware/mistake/)
- [Postbox](/docs/middleware/postbox/)
- [Route](/docs/middleware/route/)
- [Uuid](/docs/middleware/uuid/)

### Extra
These middleware are developed by the Phapi team and therefor integrates well with the Phapi Framework. These middleware are not installed by default since they are not a requirement to have a working API nor are the functionality these middleware provide needed by everyone.

- [HTTP Access Control (CORS)](/docs/middleware/cors)
- [Rate Limit](/docs/middleware/rate-limit)

### Third party
There are currently no third party middleware. [Get in contact](/contact/) if you have implemented one and want it listed here.
