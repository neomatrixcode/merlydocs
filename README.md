# Quick start

Merly is a **micro framework** for declaring routes and handling requests.                                                                       Quickly creating web applications in Julia with minimal effort.

{% hint style="danger" %}
These docs are for **Merly v1**
{% endhint %}

## Installation

First [download](https://julialang.org/downloads/#current_stable_release) and install Julia. `1.5` or higher.                                                                                                                        To do the installation use any of the following commands:

```julia
using Pkg
Pkg.add("Merly")
```

```julia
(@v1.5) pkg> add Merly
```

## Hello, World!

This is the simplest application you can do with Merly:

{% code title="server.jl" %}
```julia
using Merly

@page "/" HTTP.Response(200,"Hello World!")

start(port= 8086)
```
{% endcode %}

```julia
julia server.jl
```



