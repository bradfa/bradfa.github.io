---
layout: post
title: Exact Steps - Backups with bup to a USB disk
date: 2016-04-15
comments: false
---

I recently learned about the [bup](https://github.com/bup/bup) backup tool!
It's pretty neat.  It stores backups like git does, but deals with big files in
a fairly efficient way.

I like to do backups to an external USB disk so that I can backup more than a
single machine to a given disk and so I can take the disk with me to avoid
having all my data get lost if there's a catastrophe at a single location.  The
downside to using an external disk like this is that I use luks encryption on
the disk and it's not always plugged in, so doing something like daily backups
is slightly harder even though it can be overcome via cron jobs and by storing
a luks key on my machine(s) (such as I could encrypt a luks key with gnupg using
my Yubikey NEO to do the encryption so as to avoid storing a plaintext luks key
on my disk).

But regardless, here's my exact steps for getting started with bup:

1. Mount hard disk to /mnt/usb (you are strongly encouraged to use luks
encryption on this disk!)
2. `mkdir /mnt/usb/.bup && bup init -r /mnt/usb/.bup` to create and initialize
a .bup directory on the USB disk.  You may need to do some sudo and chmod/chgrp
action depending on how your USB disk gets mounted.  You'll save the actual
files from backups here later.
3. `bup init` to create the core bup repo in your home directory, the index
will live here
4. `bup index ~/` to index your home directory
5. `bup index /etc` to index your /etc directory
6. `bup save -n ${HOSTNAME}-etc -r /mnt/usb/.bup /etc` to save the backup of
your /etc directory to your USB disk.  This backup set will result in a branch
named after ${HOSTNAME}-etc, so that if you backup other PCs to this same .bup
directory on your USB disk, you'll be able to see each one in a separate
branch.
7. `bup save -n ${HOSTNAME}-home -r /mnt/usb/.bup ~/` to save the backup of
your home directory to your USB disk.  Similarly, your home directory will go
in a ${HOSTNAME}-home branch.

To make a future incremental backup, mount your disk and start from step 4.

If you have more than one user on a given PC, you may want to backup the entire
/home directory, or you may want to pick a more descriptive name for the backup
branch which includes the username.
