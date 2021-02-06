# BodyParser



Binds the request body to a struct. `BodyParser` supports decoding query parameters and the following content types based on the `Content-Type` header:

```
function tojson(data::String)
   return JSON.parse(data)
end

formats["application/json"] = tojson

```



```text
Post("/data", (request,HTTP)-> begin

  HTTP.Response(200
          , HTTP.mkheaders(["Content-Type" => "text/plain"])
          , body=string("I did something! ", request.body["query"]))

end)

```

