---
layout: docs
title: Request & Response
excerpt: How does the PSR-7 implementation work and how can we use it?
---

## Introduction
Phapi is [PSR-7](https://github.com/php-fig/http-message/) compliant but does not implement the interfaces itself, instead Phapi depends on the  [zend-diactoros](https://github.com/zendframework/zend-diactoros) implementation. See the PSR-7 interfaces for more information about how to use them:

- [Psr\Http\Message\ServerRequestInterface](https://github.com/php-fig/http-message/blob/master/src/ServerRequestInterface.php)
- [Psr\Http\Message\ResponseInterface](https://github.com/php-fig/http-message/blob/master/src/ResponseInterface.php)
- [Psr\Http\Message\UriInterface](https://github.com/php-fig/http-message/blob/master/src/UriInterface.php)
- [Psr\Http\Message\StreamInterface](https://github.com/php-fig/http-message/blob/master/src/StreamInterface.php)
- [Psr\Http\Message\UploadedFileInterface](https://github.com/php-fig/http-message/blob/master/src/UploadedFileInterface.php)

## Extended methods
### Body
Use the <code>withUnserializedBody(array $data)</code> method on the response object to add or modify the body. The serializer middleware will then serialize the body and set the serialized string as the response body.
