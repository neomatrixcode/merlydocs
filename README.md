# Quick start

## Getting Super Powers

Becoming a super hero is a fairly straight forward process:

```julia
               _
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.5.3 (2020-11-09)
 _/ |\__'_|_|_|\__'_|  |  Official https://julialang.org/ release
|__/                   |

(@v1.5) pkg> add Merly
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

```julia
using Merly

u= 1

useCORS()

@page "/" "Hello World!"

@page "/hola4/:usr" begin
    string("<b>Hello4 !</b>")
end

@page "/hola3/:usr" (;u=u) begin
    u = u +1
    string("<b>Hello3 ",u," !</b>")
end

@route GET "/get/data" begin
  "get this back: data"
end

@route GET "/get/u" (;u=u) begin
  u= u+1
  string("get this back:", u)
end
#bug [/get/data1 resuelve a la ruta /get/data]


Get("/test1/:usr",
	(request, response) -> begin
        string("<b>test1 !</b>")
    end
)


Get("/tes2/:usr",
    (result(;u=u) = (request, response)-> begin
    	    u= u+1
            string("<b>test2 ",u," !</b>")
        end)()
)


#middleware
function authenticate(request, HTTP)

  return request, HTTP, 300
end


@route GET "/verify" (;u=u) begin
  u= u+1
  return  HTTP.Response(200,string("<b>verify ", data, u ," !</b>"))
end


Get("/verify",

	(result(;middleware=authenticate) = (request, HTTP)-> begin

	    myfunction = (request, HTTP, data)-> begin
	              return  HTTP.Response(200,string("<b>verify ", data ," !</b>"))
	    end

	    return myfunction(middleware(request,HTTP)...)

	end)()

)


@async start()
```

{% code title="hello.sh" %}
```julia
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



