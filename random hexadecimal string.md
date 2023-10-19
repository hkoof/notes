---
tags: random, hex, string, unique, temp, tmp, uuid, simple, shell, script
---

Easy way to get a high quality random hex string on Linux:

    cat /proc/sys/kernel/random/uuid

Or, with the hyphens removed:

    sed s=-==g /proc/sys/kernel/random/uuid
