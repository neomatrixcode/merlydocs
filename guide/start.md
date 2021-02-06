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



By default, when executing the process, it will only use one processor core: if you want to use all the available cores on the machine, you can use a script that allows the process to run on all the available logical processors.

{% code title="run.sh" %}
```bash
#!/bin/sh

for i in $(seq 0 $(($(nproc --all)-1))); do
	julia --threads auto server.jl &
done

while : ; do sleep 1 ; done
```
{% endcode %}

In windows a similar script would be:

```bash
@echo off

echo %NUMBER_OF_PROCESSORS%

FOR /L %%G IN (1,1,12) DO start /B julia --threads auto myserver.jl

 timeout /t 60 /nobreak
pause
```

