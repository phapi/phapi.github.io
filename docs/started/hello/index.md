---
title: Hello API
excerpt: Last steps to get your "hello world" response working by creating your first endpoint and route.
---

## Hello API
If you've followed the Get started guide you should be able to fire off a request to the root of your URI and get a response. Please note that you must do a <code>GET</code> request and include the <code>Accept</code> header with <code>application/json</code> as the value. The response you get should look like this:

```json
{
  "message": "Welcome to the API."
}
```

## Create more endpoints
Add more endpoints to the <code>app/endpoint/</code> directory and
learn more about how to work with endpoints by reading about [endpoints in the documentation](/docs/core/endpoints/).

## Set up routes
When you've added more endpoints you also need to set up routes that points to the new endpoints. Add those routes to the <code>app/configuration/routes.php</code> file and read [more about how routes works in the documentation](/docs/core/routes/).
