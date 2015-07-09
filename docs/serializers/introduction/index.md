---
title: Serializers
excerpt: An introduction to how serializers work and how Phapi uses them
---

## Introduction to serializers
One of Phapi's features is the easy to use serializers. These makes it possible to interact with your API with any of the formats that the serializers support. It also makes it easy for you to configure your API to your needs.

## What are serializers?
Serializers are a type of middleware that transforms the data that the API sends to, and receives from the client.

## How are they used
A serializer transforms the data sent to the client to match the clients wishes (according to the <code>Accept</code> header included in the request).

In each serializer package there are also a deserializer that can transform the data a client sends to the API to a PHP array that [middleware](/docs/middleware/introduction/) and/or [endpoints](/docs/core/endpoints/) can handle. The deserializer uses the request <code>Content-Type</code> header to determine if it can handle the data included in the incoming request.

## How to implement your own
See the [implement your own serializer](/docs/implement/serializers/) section for more information.

## Existing serializers
The list of cache providers are currently quite slim but more providers will be added later on.

### Included by default
Phapi includes these serializers by default:

- [JSON](/docs/serializers/json/)

### Extra
- [XML](/docs/serializers/xml/)
- [YAML](/docs/serializers/yaml/)

### Third party
There are currently no third party serializers. [Get in contact](/contact/) if you have implemented one and want it listed here.
