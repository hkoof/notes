---
tags: [random, sleep, time, splay, infinite, infinity, forever]
---

Sleep for a random time, max 240 seconds in this case:

```bash
    sleep $(($(od -dN2 /dev/urandom | sed -n 's/[^ ]* //p') % 240))
```

To sleep forever for a infinite time to infinity:

```bash
    sleep infinity
```
