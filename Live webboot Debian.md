---
tags: [human, readable, humanize, bash, shell, script, size, file size]
---

## Debian live bootable from a webserver.

Terms:

- *"Netboot"* : Booted kernel mounts root filesystem over NFS.

- *"Webboot"* : Booted kernel download root filesystem (usually squashfs) over http.

How to create a Debian live webboot that runs a custom script at the end of
startup sequence.

Install Debian Liveboot package:
```bash
apt-get install live-build
```

At this moment (march 2024) we use the "bullseye" release of debian for the
live-boot even though it's old-stable. The current stable release has non-free
firmware packages split off into the new "non-free-firmware" archive area.  An
apparent bug related to this prevents "bookworm" live-builds from being
created. The build end with an error saying: *"E: Package 'firmware-linux' has
no installation candidate"*. A bug report on the debian mailing list seems to
suggest it's already resolved, however we still have this problem. See:
https://lists.debian.org/debian-live/2023/02/msg00000.html

Build a webbootable squashfs image:
```bash
mkdir debian_webboot
cd debian_webboot

lb config --distribution bullseye --archive-areas "main contrib non-free" -b netboot --net-root-path "/srv/debian-live"
lb build

# The resulting file needed for webboot
#
ls -hl binary/live/filesystem.squashfs
ls -hl chroot/boot/vmlinuz-5.10.0-28-amd64
ls -hl chroot/boot/initrd.img-5.10.0-28-amd64
```
