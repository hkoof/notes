---
tags: [ random, hex, string, unique, temp, tmp, uuid, simple, shell, script ]
---

Easy way to get a high quality random hex string on Linux:

```bash
    cat /proc/sys/kernel/random/uuid
```

Or, with the hyphens removed:

```bash
    sed s=-==g /proc/sys/kernel/random/uuid
```
