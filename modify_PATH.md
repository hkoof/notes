---
tags: [modify, PATH, $PATH, environment variable, script, bash]
---


```bash
path_remove()  {
    local p=${PATH//${1}}
    p=${p#:} ; p=${p%:}
    export PATH=${p//::/:}
}

path_append() {
    path_remove $1
    export PATH=$PATH:$1
}

path_prepend() {
    path_remove $1
    export PATH=$1:$PATH
}
```
