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



## useCORS

The useCORS method allows you to configure the parameters with which CORS will be enabled, which are: 

* **AllowOrigins**: Specify a URI that can access the resource. The explorer must ensure this. For requests without credentials, the server must specify `*` as a wildcard, thus allowing access to the resource from any source. 
* **AllowHeaders**: indicates which HTTP header can be used when requesting the resource. The wildcard  `*` allows all headers. 
* **AllowMethods**: Specifies the method or methods allowed when a resource is allocated. 
* **MaxAge**: This header indicates for how long the results of the verified request can be captured, and therefore it is no longer necessary to carry out the process again. 

The default values with which the method operates are:

```julia
useCORS(
AllowOrigins = "*"
, AllowHeaders = "Origin, Content-Type, Accept"
, AllowMethods = "GET,POST,PUT,DELETE"
, MaxAge = "178000")
```





