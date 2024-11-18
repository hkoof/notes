---
tags: [atomic, unique, serial number, shell, bash]
---

## Atomic serial numbers in bash

Creating serial numbers in bash that are unique even when multiple processes
running the script in parallel:

```bash
new_serial_number()
{
    local serial_num_file=/tmp/.last_serial_num
    {
        flock --timeout 2 -x 9 || return 1
        lastnum=$(<${serial_num_file})
        newnum=$((lastnum + 1))
        echo "$newnum" >${serial_num_file}
        printf '%012d' "$newnum"
    } 9<>${serial_num_file}
}
```
