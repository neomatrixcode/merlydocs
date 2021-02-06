---
description: >-
  The start function allows to take off the files in a specific IP address and
  port.
---

# Start

## Configuration

The start function takes three parameters.

* **host**: IP address where the process will listen, you can use the ipv4 protocol such as ipv6, it is specified with a string
* **port**: the port number where the process will listen, it is indicated with an integer number.
* **verbose**: allows you to view the events processed by the process in real time, indicated with a boolean value

The default values that the function receives are:

```julia
start( host = "127.0.0.1", port = 8086, verbose = false)
```



By default, when executing the process, it will only use one processor core.

## TLS

To enable TLS / HTTPS the **sslconfig** parameter is used, which receives the https certificate files.

{% hint style="info" %}
If you want to generate HTTPS certificate for localhost domains, you can follow the following [tutorial](https://gist.github.com/cecilemuller/9492b848eb8fe46d462abeb26656c4f8).
{% endhint %}

```julia
using MbedTLS

start( sslconfig= MbedTLS.SSLConfig("localhost.crt", "localhost.key") )
```



