---
description: 'webserverfiles allows serving static files like images, CSS, and JavaScript.'
---

# Statics files

## webserverpath

The webserverpath method allows to set a certain folder or path as the current or base directory.

```julia
 webserverpath("folder") 
```

## webserverfiles

The webserverfiles method allows you to indicate if all the existing files in the directory considered as base or current will be exposed, or specify which files will be exposed by means of their extension.

* **`*`** : Exposes all files located in the path considered as base, except those that start with `.`
*  **`css|js|html`** : Extension in files that will be exposed

```julia
webserverfiles("*")
```

## File

The File method allows to obtain the content of a file located in the base or current directory, receives a string with the name and extension of the file and returns a string with its content.

```julia
File("index.html")
```



