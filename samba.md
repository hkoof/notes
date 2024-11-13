---
tags: [samba, smbclient, winbindd]
---

## Samba client

### Using smbclient

```bash
smbclient //<server>/<share> -U <username>
```

### From Windows

Specify this UNC:
```
\\<server>\<share>
```

## Samba server side

Listing accounts known by `winbind`:

```bash
wbinfo -u
```


