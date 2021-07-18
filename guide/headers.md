---
description: It is possible to configure the headers returned by the framework
---

# Headers

The headers are returned on each endpoint within each HTTP structure.



```julia
HTTP.Response(200
          , HTTP.mkheaders(["Content-Type" => "text/plain"])
          , body="I did something!")
```



However, if you need to always return a certain or certain headers in each route, to avoid unnecessary code repetition you can use the headersalways function, in the same way there is a method that allows you to configure CORS.

## headersalways

It is a method that allows you to establish a headre or set of headers that will be returned as soon as a request is made to any endpoint. The headers will be placed in a row of tuples, these can be one or more headers.

```julia
headersalways(["X-PINGOTHER" => "pingpong", "Y-PINGOTHER" => "text"])
```

