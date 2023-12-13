---
tags: [bash, xargs, function]
---

```bash
# Print 5 packages on each line
# to emulate xargs -n 5
# This can be useful when you would want to call a shell function
# using xargs.

package_list=./package_list.txt

chunk_size=5
list_chunk=()
while read pkg ; do
    list_chunk+=($pkg)
    if ! (( ${#list_chunk[*]} % chunk_size)) ; then
        echo "${list_chunk[*]}"
        list_chunk=()
    fi
done < $package_list
[[ ${list_chunk[*]} ]] && echo "${list_chunk[*]}" 
```
