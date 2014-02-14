---
layout: post
title: Debootstrapping a chroot
date: 2014-02-14
comments: false
---

Chroots are very useful for keeping software that does stupid things from
affecting your main system (like TI's CCSv5) or for running old software safely
without needing a virtual machine, so long as you can do so with the existing
kernel.  I use them on a regular basis to run CCSv5, software from Debian
Squeeze, and to try things out with low risk.

Quick exactsteps for debootstrap and schroot on Debian in order to run oldstable
or similar:

Install debootstrap and schroot:

    sudo apt-get install debootstrap schroot

Make a directory for your chroot, I use `/opt`:

    sudo mkdir -vp /opt/chroot/squeeze

Debootstrap!  Using the `buildd` variant to get usual software building tools:

    sudo debootstrap --variant=buildd --arch=amd64 squeeze /opt/chroot/squeeze

Setup schroot:

    cat >> /etc/schroot/schroot.conf << "EOF"
    [squeeze]
    description=Squeeze
    type=directory
    directory=/opt/chroot/squeeze
    users=andrew
    preserve-environment=true
    EOF

Then you can schroot into your Squeeze system:

    schroot -c squeeze

If you're using Debian's normal $PS1, your shell prompt will show a description
of which schroot you're in, like:

    (squeeze)andrew@boomboom:/tmp$

If your user is in the `sudo` group, and if you have sudo installed in your
schroot, you'll be able to use sudo just like normal.  To add extra packages to
the schroot system during the debootstrap operation, add `--include=sudo` or
similar prior to the "squeeze".  Alternatively, you can install software with
apt afterwards like normal.

Be aware, by preserving the environment, your `/home` directory will be your
actual home directory in the chroot.  The rest of the root file system won't be
related to your actual root file system, though.  Just be careful!
