---
tags: [ bash, script, tmpdir, tmp, temp, directory, cleanup ]
---

```bash
    script=${0##*/}
    tmp=$(mktemp --tmpdir -d "${script}.XXXXXXXXXX")
    trap "rm -r $tmp" EXIT
```

Note that there is no need to specify INT QUIT TERM [...] when they will just
exit. EXIT handler will be invoked too in that case.
