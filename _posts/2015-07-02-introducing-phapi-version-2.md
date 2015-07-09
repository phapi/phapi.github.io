---
title: Introducing Phapi version 2
permalink: /blog/introducing-phapi-version-2
tags:
  - psr7
  - middleware
  - documentation
author:
  name: Peter Ahinko
---

It's with great pleasure I'm able to introduce the second version of the Phapi Framework. Soon after the first version was released I realized that I wanted to make Phapi [PSR-7](http://www.php-fig.org/psr/psr-7/) compliant and use an middleware driven architecture. Version 1 did support middleware but the core application was no where nere an architecture that heavily relied on middleware.

<!--more-->

The [list of available middleware](/docs/middleware/introduction/) is short at the moment but this is a conscious decision. The core application consists of the functionality and features that's needed to create an API. But there are many more features that you might want to have, but since not everyone want or needs the same features these features will be developed as separate packages that can easily be installed when needed.

## Middleware
As just mentioned above Phapi has an architecture where almost everything is a middleware. The error handling, serializers, routing, content negotiation and much more is all middleware.

The benefits with middleware are many:

- It's **easy to understand** and write your own middleware.
- It's **easy to use** and add new features and new functionality when needed since you only need to add it to the pipeline.
- **Reusable**, use middleware written for other frameworks and solutions as long as they have the same method signature.
- **Performance**, the whole application doesn't have to be executed if an early middleware can return the proper response.

## Documentation
[Documentation](/docs/) is always tricky since it always can be better. With version 2 the documentation has improved dramatically. That does however not suggest that it's perfect or finished. The documentation will keep getting better and better. I'm thinking of adding a **tutorials** section with in depth documentation on how to install and use certain features.

## What's next?
The list of thing I wan't to add to the framework is extensive but I don't want to reveal to much right now.

## Contribute
Help is always welcome. As I mentioned before the documentation can always be better. Even the smallest things like correcting grammar is welcome.

I would love to add your packages to the [list of available packages]() if you implement your own middleware, serializer or cache provider.

See the [contributions](/docs/contributions/) page for more information about how to contribute.
