---
tags: [ buffer, stdout, pty, terminal, expect pipe]
---

Tools to "unbuffer" a pipe:

- The `unbuffer` command which is part of the `expect` utility. On Debian the command is `expect-unbuffer`.

- The `stdbuf` util. See: https://www.gnu.org/software/coreutils/manual/html_node/stdbuf-invocation.html


For example to disable 4k pipe buffering to create your own progress bar, like so:

```bash
    unbuffer program | my_progressbar_script
```
