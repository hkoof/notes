---
tags: LDIF, ldif, space, unwrap, wrapped, lines, start/space
---

File in LDIF format wrap lines by starting the next line with exactly one
space. To unwrap, use this perl command:

```perl
    perl -e '$f = do { local $/; <> }; $f =~ s/\n //gms; print $f;' example.ldif
```
