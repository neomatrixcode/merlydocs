---
description: La funcion de
---

# Start

## Getting Super Powers

Becoming a super hero is a fairly straight forward process:

```
start( host = "127.0.0.1", port = 8086, verbose = false)
```



```text
#!/bin/sh

for i in $(seq 0 $(($(nproc --all)-1))); do
	julia --threads auto server.jl &
done

while : ; do sleep 1 ; done
```



