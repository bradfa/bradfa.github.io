---
layout: post
title: A Few Debian Notes (live, wicd, and encfs)
date: 2012-06-28
comments: false
---

I installed Debian Squeeze this morning and used a few resources I hadn't
known of before.  The install went well and I'd recommend taking a look at
these:

The [Debian Live Project][1] has rather nice live CDs for Debian. I tried
out the LXDE desktop one and found I rather like LXDE, it runs rather quick
on my really old Dell Inspiron 9300 laptop.  The ISO won't fit on a CD (boo!)
but DVD-Rs or USB flash drives are rather easy to come by.

[wicd][2], the wireless interface connection daemon, is a very nice replacement
for network-manager.  wicd will do basically the same thing as network-manager
but without needing Gnome.

And lastly, [encfs][3].  Encrypt your home directory and have it decrypt
automatically on login.  Not super hard to setup, just be sure to read the
instructions carefully.  I prefer encfs over full lvm encryption as when
installing on flash memory media (like an ssd or USB flash drive), you can
simply create normal partitions aligned to the erase block size.  Also, you
can have a setup where you only have one giant root partition but want some
directories within it to be encrypted, removing the need for lvm in order
to get encryption.

[1]: http://live.debian.net/
[2]: http://wiki.debian.org/WiFi/HowToUse#Wicd
[3]: http://wiki.debian.org/TransparentEncryptionForHomeFolder
