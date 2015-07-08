---
title: Documentation
excerpt: Welcome to the documentation of the Phapi Framework. Learn more about how to configure, use and extend the framework.
---

## The Phapi Framework
Phapi is a PHP based framework aiming at rapid and simplified API development as well as focusing at performance and keeping the code base small and simple.

## Philosophy
Phapi is developed with the following aspects in mind: keep it simple, flexible and easy to use as well as small and high performance.

It's heavily based on middleware. The advantages with middleware is that it's easy to add and remove functionality as well as keeping the performance as high as possible since the whole pipeline doesn't always have to be executed if a middleware early in the pipeline can return an expected response.

Modifying the functionality of Phapi is really easy. If you don't need one of the basic functionality thats included in Phapi, just remove the middleware. If you are missing a functionality you can just add a middleware that handles the desired functionality.

More middleware than those included in the basic configuration can be found in the [directory of extra middleware](/docs/middleware/introduction/) that is developed by the team behind Phapi. There is also a [directory of third party middleware](/docs/middleware/introduction/) and it's also really easy to [write your own](/docs/implement/middleware/).

## Application workflow
The application workflow can be broken down to the following steps:

- configure the application
- set up the request and create an empty response
- set up the middleware pipeline
- run the middleware pipeline, middleware will be invoked from the outside in, in the order they are added
- the route middleware will try to dispatch to an endpoint
- the middleware pipeline will traverse back from the inside out
- the response will be returned to the client

Note that a middleware can stop the traversing at any time. As an example a authentication middleware can return an error if the client isn't allowed to access the requested resource.

## PSR (PHP Standard Recommendations)
Phapi are and always will be compliant to as many [PSRs](http://www.php-fig.org/psr/) as possible. If the Phapi Framework can take advantage of a PSR it will. Phapi is currently compliant to these PSRs:

- [PSR-1: Coding Standard](http://www.php-fig.org/psr/psr-1/)
- [PSR-2: Coding Style Guide](http://www.php-fig.org/psr/psr-2/)
- [PSR-3: Logger Interface](http://www.php-fig.org/psr/psr-3/)
- [PSR-4: Autoloading](http://www.php-fig.org/psr/psr-4/)
- [PSR-7: Http Message](http://www.php-fig.org/psr/psr-7/)

## Contact
See the [Get in contact](/contact/) page.

## License
The MIT License (MIT). Please see the [License File](https://github.com/phapi/phapi/blob/master/license.md) for more information.
