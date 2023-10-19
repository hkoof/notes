---
tags: tmux,detach,client,other
---

##### detaching other clients from a tmux session

`tmux kill-server` can be used to detach *all* clients, shutdown all sessions
and exit the server.

If you're inside a tmux session, you can use `:kill-session -a` to kill the
sessions of all other clients.

