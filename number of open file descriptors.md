---
tags: file, handles, open, descriptors, proc, max
---

The file `/proc/sys/fs/file-nr` contains:

```bash
    <number of open file descriptors> 0 <max number of open file descriptors>
```

(the second number is always zero (0) on kernel v2.6 or later)
