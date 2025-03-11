---
tags: [ bash, history, features, unlimited, deduplicate, eternal ]
---

```bash
# Eternal bash history.
# ---------------------
# Undocumented feature which sets the size to "unlimited".
# http://stackoverflow.com/questions/9457233/unlimited-bash-history
export HISTFILESIZE=
export HISTSIZE=
export HISTTIMEFORMAT="[%F %T] "
# Change the file location because certain bash sessions truncate .bash_history file upon close.
# http://superuser.com/questions/575479/bash-history-truncated-to-500-lines-on-each-login
export HISTFILE=~/.bash_eternal_history
# Force prompt to write history after every command.
# http://superuser.com/questions/20900/bash-history-loss
PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```

Use this to keep shell history separate per session (based on hostname and tty
name). Of course create ~/hist directory first.

```bash
export HISTFILE="/home/$USER/hist/`uname -n``tty | tr '/' '-'`"
```


