---
layout: post
title: FTDI USB Serial Device Naming
date: 2020-07-16
comments: false
---

I have multiple of the exact same FTDI USB to serial interface cables attached
to my PC and I wanted to name them physically and within Linux.  I solved the
physical part with a label maker but I also want the device names to match up.

To do this I created a special udev rule which names each interface based on its
USB serial number.  Then when I plug in the "BOARD1" cable it will show up as
/dev/ttyBOARD1 consistently.

```
$ cat /etc/udev/rules.d/ftdi.rules 
SUBSYSTEMS=="usb", KERNEL=="ttyUSB*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="ABCD1239", SYMLINK+="ttyBOARD1"
```
