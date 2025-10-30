---
layout: post
title: Encrypted Swap Initramfs Generation Complaints
date: 2025-10-30
comments: false
---

Most of my computers use a random key with cryptsetup and LUKS2 to encrypt
their swap partitions.  This works fine but it does mean that hibernation may
not work.  But doing this will cause ugly warnings during boot and when
upgrading kernels.

The kernel upgrade warnings will look like:

```
Processing triggers for initramfs-tools (0.148.3) ...
update-initramfs: Generating /boot/initrd.img-6.12.48+deb13-amd64
cryptsetup: WARNING: swap: couldn't determine device type, assuming default
    (plain).
cryptsetup: WARNING: Resume target swap uses a key file
Updating kernel version 6.12.48+deb13-amd64 in systemd-boot...
```

To resolve both of these issues, we need to just tell the initramfs generation
tooling that we don't want nor have a "resume" device:

```
$ echo "RESUME=none" | sudo tee /etc/initramfs-tools/conf.d/resume
```

Then we can rebuild the initramfses:

```
$ sudo update-initramfs -u -k all
```

On reboot, this should resolve both issues.

Hibernation will not work, but that's OK for me.  If you need hibernation to
work and you want encrypted swap, you need to use a non-random key for it and
then this blog article doesn't apply to you.
