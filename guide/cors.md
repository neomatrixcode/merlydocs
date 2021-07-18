# CORS

The useCORS method allows you to configure the parameters with which CORS will be enabled, which are:

* **AllowOrigins**: Specify a URI that can access the resource. The explorer must ensure this. For requests without credentials, the server must specify `*` as a wildcard, thus allowing access to the resource from any source. 
* **AllowHeaders**: Indicates which HTTP header can be used when requesting the resource. The wildcard  `*` allows all headers. 
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



