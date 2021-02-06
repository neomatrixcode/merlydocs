---
description: Routing refers to the way an application's endpoints are defined.
---

# Routing

## Paths

Route paths, combined with a request method, define the endpoints at which requests can be made. 

The routes are created with the name of an http verb \(GET, POST, PUT, DELETE, etc.\), a string that establishes the path of the endpoint and a function, which receives a pair of parameters and returns an HTTP response structure.

* **request**: Contains all the data sent by the client.                                                                                                                The query string, the body, the headers and the params.

```julia
"/data?hola=1" #url query
```

* **HTTP**: Create an http response. It will host the http code, the response body and the http headers.

```julia
(request,HTTP)-> begin
   return HTTP.response(200, "test text Post")
end
```

The @page macro establishes a GET method by default, it is only required to specify the body of the function, the request and HTTP parameters are passed implicitly.

```julia
@page "/" HTTP.Response(200,"Hello World!")
```

The macro @route is similar to @page with the difference that @route allows you to explicitly set the HTTP verb to use

```julia
@route GET "/route" HTTP.Response(200, "I did something!")
```

It is possible to link several HTTP verbs to a single function using the operator `|` . 

```julia
@route POST|PUT|DELETE "/route" begin
  println("query: ",request.query)
  println("body: ",request.body)

  HTTP.Response(200
          , HTTP.mkheaders(["Content-Type" => "text/plain"])
          , body="I did something!")
end
```

Macros aren't the only ways endpoints can be set; you can also use functions, which receive the name of the endpoint as a string and the function to be executed.

```julia
Get("/data", (request,HTTP)->begin
    HTTP.response(200, "test text Get")
end)

Post("/data", (request,HTTP)-> begin
    HTTP.response(200, "test text Post")
end)

 Put("/data", (request,HTTP) -> begin
     HTTP.response(200, "test text Put")
 end)
 
 Delete("/data", (request,HTTP) -> begin
     HTTP.response(200, "test text Delete")
 end)
 
 Connect("/data", (request,HTTP) -> begin
     HTTP.response(200, "test text Connect")
 end)
 
 Trace("/data", (request,HTTP) -> begin
     HTTP.response(200, "test text Trace")
 end)
 
 Head("/data", (request,HTTP) -> begin
     HTTP.response(200, "test text head")
 end)
 
 Patch("/data", (request,HTTP) -> begin
     HTTP.response(200, "test text Patch")
 end)
```

## Route parameters

Route parameters are dynamic elements in the route, which are named segments using the symbol `:` or without a name. They are placed in the name of the url and it is compatible with the previously mentioned methods of creating endpoints.

The obtained values can be retrieved using the params dictionary stored in the request variable, with the path parameter name specified in the path.

```julia
@page "/hola/:usr" begin
HTTP.Response(200,string("<b>Hello ",request.params["usr"],"!</b>"))
end

@route GET "/get/:data1" begin
  HTTP.Response(200, string(u ,request.params["data1"]))
end

Get("/test1/:usr",
  (request, HTTP) -> begin
        HTTP.Response(200,string("<b>test1 ",request.params["usr"],"!</b>"))
    end
)
```

It is also possible to use a [regular expression](https://docs.julialang.org/en/v1/manual/strings/#Regular-Expressions) to specify the parameters in a custom way and it can be retrieved by the position of the parameter in the path.

```julia
@route GET "/regex/(\\w+\\d+)" begin
  return HTTP.Response(200, string("datos ",request.params["2"]))
end
```

## Variables

It is possible to pass program variables to functions. In the case of macros, the variables will be passed through a list of parameters separated with commas and starting with `;` . On the right side of the  `=` symbol, the name of the variable to be entered will be placed and on the left side the name will be placed as it will be invoked or used within the function.

```julia
@page "/get1" (;u=u) HTTP.Response(200,string("<b>Get1 ",u," !</b>"))


@route GET "/get/:data1" (;u=u) begin
  u = u +1
  HTTP.Response(200, string(u ,request.params["data1"]))
end
```

{% hint style="warning" %}
Depending on whether the data is mutable or not, we will get a step by reference or a step by value. 

In case the parameters are not mutable, they are passed by value, therefore, it can be modified safely in the function, the same happens with primitive variables such as an integer. 

On the other hand, when they are mutable, like a vector, they are passed by reference, so if they are modified within the function they will also be modified outside. 
{% endhint %}

It is possible to use the function format to enter variables.

```julia
Get("/test2/:usr",
    (result(;u=u) = (request, HTTP)-> begin
          u= u+1
          HTTP.Response(200,string("<b>test2 ",u,request.params["usr"]," !</b>"))
        end)()
)
```

if the variable is read-only, it is possible to use it in the simple function format just by invoking it; but if you want to modify it you should use the `global` reserved word, however it is not recommended due to loss of performance.

```julia
Get("/data", (request,HTTP)->begin

  HTTP.Response(200
          , HTTP.mkheaders(["Content-Type" => "text/plain"])
          , body=string(u,"data ")

end)


Post("/data", (request,HTTP)-> begin

  global u="bye"

  HTTP.Response(200
          , HTTP.mkheaders(["Content-Type" => "text/plain"])
          , body=string("I did something! ")

end)
```



