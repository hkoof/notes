---
tags: [human, readable, humanize, bash, shell, script, size, file size]
---

    humanize()
    {
	    numfmt --to=iec --format=%.1f $((${1} * 1024)) 
    }
    
The other way around, interpret human readable (file) size to get a canonical number of bytes:

    ezinamuh()
    {
        echo $(( $(numfmt --from=iec ${1}) / 1024 ))
    }
