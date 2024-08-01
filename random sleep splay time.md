---
tags: [ random, sleep, time, splay, infinite, infinity, forever ]
---

Example sleep for 0.0 - 1023.9 seconds ( ~ 17 minutes)

```bash
sleep $((RANDOM >> 6)).$((RANDOM % 10))
```

Example sleep for a random time, max 240 seconds in this case:

```bash
sleep $(($(od -dN2 /dev/urandom | sed -n 's/[^ ]* //p') % 240))
```

To sleep forever for a infinite time to infinity:

```bash
    sleep infinity
```
