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

The webserverfiles method allows you to indicate whether all the existing files in the directory considered as base or current will be exposed, or otherwise specify which files should not be exposed, by means of their extension.

* **`*`** : Exposes all files located in the path considered as base, except those that start with `.`
*  **`jl`**  : File extension that should not be exposed
*  **`clj|jl|py`** : Extension in files that will not be exposed

```julia
webserverfiles("*")
```



