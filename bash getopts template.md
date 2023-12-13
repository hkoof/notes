---
tags: [bash,getopts,example,script,template]
---

```bash
#!/bin/bash
#

usage()
{
    exitcode=${1:-0}
    if [ "$exitcode" != 0 ] ; then
        exec >&2
    fi

    echo "Usage: ${0##*/} [OPTIONS] ARG"
    exit $exitcode
}

unset option_s option_Q

while getopts "hsQ:" option ; do
    case $option in
        '?')        usage 2 ;;
        'h')        usage ;;
        's')        option_s=1 ;;
        'Q')        option_Q=$OPTARG ;;
    esac
done
shift $(($OPTIND - 1))
[[ "$#" -lt "1" ]] && usage     # At least 1 ARG required

[[ $option_s ]] && echo "Option -s was specified"
[[ $option_Q ]] && echo "Option -Q was specified with argument: $option_Q"

while [[ $1 ]] ; do 
    echo "ARG: $1"
    shift
done
```
