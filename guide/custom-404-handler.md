---
description: It is possible to return a personalized message when a route cannot be found.
---

# Custom 404 Handler

## notfound

The notfound method allows you to customize the response of the 404 error code, it is possible to pass the html code in string format to the method.

```julia
notfound("""<!DOCTYPE html>
              <html>
              <head><title>Not found</title></head>
              <body><h1>404, Not found</h1></body>
              </html>""")
notfound("website/notfound.html")
```

It is also possible to pass a path that includes the name of the html file to use. The path will start from the directory where the program is located or from the path specified as a base.

```julia
notfound("folder/notfound.html")
```





