
---
tags: [grub, rescue, live, chroot, grub-install, bind mount, mount, device, mbr, chris]
---


```
# where sda1 is the root partition
mount /dev/sda1 /mnt
mount -t proc none /mnt/proc
mount -t sysfs none /mnt/sys
mount -o bind /dev /mnt/dev
mount -o bind /tmp/ /mnt/tmp

# chroot into your installation
chroot /mnt /bin/bash

# and, if also needed, re-install grub with the bios packages only
apt-get --reinstall install grub-common grub-pc os-prober

# if there is an error repeat the setup via:
grub-install --recheck /dev/sda
```