---
layout: post
title: BeagleBone LEDs with Arago Kernel v3.2
date: 2012-03-01
comments: false
---

If you boot your BeagleBone using the supplied micro SD card image, there are
two LEDs (near the Ethernet jack) that will blink.  D2 (USR0 on the schematic)
will blink a heart beat, and D3 (USR1 on the schematic) will blink on SD card
access.

This is really handy.  Since the Linux kernel is actually performing the blink
operations, as long as the heart beat is going, the kernel is running.  And if
your BeagleBone is not responding well, but the SD card access LED is flashing
like there's no tomorrow, it's just because SD cards are slow and a lot of disk
access is going on.

But if you want to run TI's [AM335XPSP_04.06.00.06 kernel] [1] from the
[Arago Project] [2], these LED actions aren't enabled by default.

To enable them, you'll need a [small patch] [3].  This is cobbled together from
code I found from the [beagle-borg] [4] team, but with portions not applicable
to the base BeagleBone removed.

I'm running Debian 6 Squeeze armel on my BeagleBone.  I now have **blinkin'
lights!**

[1]: http://arago-project.org/git/projects/?p=linux-am33x.git;a=shortlog;h=refs/heads/AM335XPSP_04.06.00.06
[2]: http://arago-project.org/wiki/index.php/Main_Page
[3]: https://gist.github.com/1950437
[4]:http://code.google.com/p/beagle-borg/source/browse/kernel/arch/arm/mach-omap2/board-am335xevm.c?spec=svn24c36edc3e53fb59cb703b08be8d25cecf548413&r=24c36edc3e53fb59cb703b08be8d25cecf548413
