---
tags: [bind,mount,findmnt]
---

Bind mounts are almost like hardlinks. The `mount` command does not show which directory is bind mounted. However `/proc` does seem to have information on the bind-mounted which the command `findmnt` can show.