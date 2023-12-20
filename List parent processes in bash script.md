---
tags: [ bash, script, pid, ppid, parent, processes ]
---

```bash
    # List parent processes up to PID 1 (exclusive)
    #
    # Args:
    #   [<pid>]  # defaults to $$
    #
    # Output: <pid> <command name> <args>
    #
    parents_processes()
    {
        local pid ppid cmd _
        pid=${1:-$$}
        while [[ $pid != 1 ]] ; do
            [[ -d /proc/$pid/ ]] || return 1
            read _ cmd _ ppid _ < /proc/$pid/stat
            echo "$pid ${cmd//[)(]}"
            pid=$ppid
        done
    }
```
