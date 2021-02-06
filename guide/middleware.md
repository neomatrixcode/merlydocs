---
description: >-
  It is possible to execute functions before or after the function associated
  with an endpoint, this in order to reprocess certain data or carry out
  previous validations.
---

# Middleware

## Getting Super Powers

It is possible to create a custom function that is executed before or after the function associated with an endpopint, the function will be created with the desired name and later it will be passed as a variable.

```julia
function authenticate(request, HTTP)
  isAuthenticated = false

  if (request.params["status"] === "authenticated")
    isAuthenticated = true
  end

  return request, HTTP, isAuthenticated
end
```

The execution of the middleware can only be achieved with the funcionm format, it cannot with the `@route` and `@page` macros. The following structure must be specified where myfunction is the function associated with the path `"/ verify /: status"`. In line number 13, the order in which the functions will be executed is indicated, first the **`middleware`** function and then the **`myfunction`** function.

```julia
Get("/verify/:status",

  (result(;middleware=authenticate) = (request, HTTP)-> begin

  myfunction = (request, HTTP, isAuthenticated)-> begin

      if (isAuthenticated == false )
          return  HTTP.Response(403,string("Unauthenticated. Please signup!"))
      end
          return  HTTP.Response(200,string("<b>verify !</b>"))
      end

  return myfunction(middleware(request,HTTP)...)

  end)()

)
```





