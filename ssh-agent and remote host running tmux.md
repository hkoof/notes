---
tags: [ssh,ssh-agent,tmux,socket,forwarding]
---

Formwarded ssh-agent to a remote host with lingering ssh sessions inside that
would like to use the ssh-agent normally fails when connecting next time.

Solution:

Put this in `~/.bashrc` on the remote host:

```bash
# Make ssh-agent work again after new ssh session attaching to an existing tmux session
#
AGENT_SOCK=$HOME/ssh-agent_${USER}.sock
if [[ $SSH_AUTH_SOCK ]] && [[ $SSH_AUTH_SOCK != $AGENT_SOCK ]] ; then
    ln -sf $SSH_AUTH_SOCK $AGENT_SOCK
    export SSH_AUTH_SOCK=$AGENT_SOCK
fi
```

