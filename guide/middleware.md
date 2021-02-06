# Middleware

## Getting Super Powers

Becoming a super hero is a fairly straight forward process:

```
function authenticate(request, HTTP)
  isAuthenticated = false

  if (request.params["status"] === "authenticated")
    isAuthenticated = true
  end

  return request, HTTP, isAuthenticated
end
```

```bash
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





