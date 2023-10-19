---
tags: bash, script, tmpdir, tmp, temp, directory, cleanup
---

    script=${0##*/}
    tmp=$(mktemp --tmpdir -d "${script}.XXXXXXXXXX")
    trap "rm -r $tmp" EXIT
    # No need to specify INT QUIT TERM when they will just exit
