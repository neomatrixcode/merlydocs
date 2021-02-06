---
description: >-
  The data sent sent in the body of a request of a client, can be processed
  previously.
---

# Body parser

## formats

If you want to format the data sent in the body by the client to an endpoint, to be used in a certain format within the body of the function that processes said request, you should only use the formats dictionary.

To this dictionary, the value of the Content-Type of the sent data will be added as a key and it will be associated with a custom method, which must necessarily receive a string and return a single value, which will be the data already processed.

```julia
function tojson(data::String)
   return JSON.parse(data)
end

formats["application/json"] = tojson

```

Once this is done, when the server is executed, the data with the respective Content-Type specified previously will be processed by the custom function and sent to the function associated with the determined endpoind.

```julia
Post("/data", (request,HTTP)-> begin

  HTTP.Response(200
          , HTTP.mkheaders(["Content-Type" => "text/plain"])
          , body=string("I did something! ", request.body["query"]))

end)

```

{% api-method method="post" host="" path="/data" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="query" type="string" required=false %}
text
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
"I did something! text"
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

