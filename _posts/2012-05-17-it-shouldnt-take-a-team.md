---
layout: post
title: It Shouldn't Take a Team
date: 2012-05-17
comments: false
---

It shouldn't take a team of engineers to build a functional embedded GNU/Linux
system on a dev kit.  Often, it does.  The embedded dev kit industry is broken.

The folks over at [Beagleboard.org][1] are hard at work fixing this, but it
takes time, and they only offer solutions based on TI SoCs.  They're doing an
awesome job, please keep it up!

But, unless you want to base an embedded design on a part that requires package
on package memory, the Beagles aren't quite there yet in terms of an open dev
kit that's as easy to use as it should be.  If you're building a multimedia
system and want a dev kit, pick a Beagleboard-xM or a Pandaboard.  Both are
great systems and have awesome support from all required software that you'll
want to run.

But if you're not trying to build a multimedia system, the Beagleboard.org team
only has the Beaglebone to offer.  Don't get me wrong, the Beaglebone is great.
However, there are currently huge nits to pick with it, and TI in general.

The [AM335x][2] SoC used on the Beaglebone is not well supported by any
mainline Linux kernel.  Even the [linux-omap][3] repo can't yet build a kernel
for an AM335x system that will enable MMC, which makes running the Beaglebone
away from an NFS root system rather difficult.  TI offers their [Arago kernel][4],
but until about 2 weeks ago, not even all of the interrupts were enabled in that
codebase.  And this is the TI kernel tree that forms the basis of TI's official
SDK releases!  To top it all off, TI has missed the Linux 3.5 window in the
linux-omap repo to get any more changes in before Linus' 3.5 merge window opens.
So, Linux 3.5 very likely won't support the AM335x very well, if at all.

Hopefully TI will be able to get code into linux-omap for the 3.6 merge, but
with that kind of timeline, AM335x won't run a mainline Linux kernel until
almost the end of 2012 (3.6 will probably be released in the 4th quarter, if
past release performance indicates future success).  The Beaglebone was on sale
in the 4th quarter of 2011.  If 1 year between release of dev kits and mainline
Linux support is considered good, that's a horrible state of "good."

AM335x silicon is due to be finalized and parts actually available for general
consumption "real soon now."  TI doesn't seem to have intentions of moving their
Arago kernel repo past a Linux 3.2 base.  Which is OK, Ben Hutchings is keeping
the v3.2.y stable series around for a while (Ubuntu and Debian rely on it), but
the Arago repo isn't run by many people, so it doesn't get very wide spread
testing.  This leads to things like [PREEMPT breaking Ethernet!][5]  Which is
reported to be in the stages of being fixed, but may or may not yet be complete.

TI's ability to push code into mainline Linux is so bad that even the
official [Beaglebone kernel][6], maintained by Koen, is diverging from TI's Arago
repo.  Granted, a good bit of Koen's changes are to support capes, but there
are fundamental changes to core AM335x code in Koen's tree that are different
than what's in Arago's.

TI needs to fix their development process, they need to have support in mainline
Linux ASAP after announcement of new SoCs.  Anything else is unacceptable.

To pick on TI even more, there's the [Craneboard][7].  Oh, my, goodness!
The Craneboard uses TI's AM3517 processor.  The AM3517 was released about
TWO YEARS AGO.  You cannot currently build a mainline Linux kernel for the
AM3517!  Even the linux-omap tree couldn't do it well, until recently, but I
haven't personally tried very hard, so it may not even do it well.  TI's
official SDK supplies a 2.6.37 kernel, which is not a long term supported
kernel.  The [Craneboard Github repo][8] is woefully out of date.

So now that I've picked on TI quite a bit, here's my stance:

I want to build a product that uses an ARM SoC and runs Linux.  I want to have
one, yes, that's right ONE single, engineer who spends only part of their time
getting cross compilers, boot loaders, Linux kernel, and the rest of the
required userspace set up.  I want that engineer to be able to receive a dev
kit from the UPS person and have it running GNU/Linux within 1 week.  Not just
running the provided SD card or what-have-you, but building all the components
from supported mainline repositories and understanding the build systems.
Documentation is a huge part of this, but core code support needs to come first.
Without mainline, whether it be Linux, u-boot, or anything else, I have nothing.

Things in this relm are getting better, but too slowly.  I put this blame
entirely on the SoC vendors, TI, Freescale, Samsung, ST, etc.  All aren't to
blame in the same amount, but all are guilty.  The pay-for Linux vendors aren't
helping, they have no incentive to make things easier for people who aren't
their customers, so I'm not looking for them to make strides here.  The SoC
vendors do have a very high vested interest in making things better, [Linaro][9]
is on the right track.

Groups like [Beagleboard.org][1] are making things better, but they are a tiny
team taking on the world and supporting not only documentation and code, but
trying to sell boards and do so on a shoe-string budget, all while making a
profit and not stepping on too many TI toes.  There needs to be more
organizations like [Beagleboard.org][1], putting out low cost dev kits and
pushing the SoC vendors to get their kernel code mainlined.

It shouldn't take a team of engineers to get Linux running on a dev kit.
If your company has a team, or pays a team, that's a sign that the dev kit
and SoC vendor industries are broken.  Let's fix that.

[1]: http://beagleboard.org/
[2]: http://www.ti.com/product/am3359
[3]: https://git.kernel.org/?p=linux/kernel/git/tmlind/linux-omap.git
[4]: http://arago-project.org/git/projects/?p=linux-am33x.git;a=shortlog;h=refs/heads/v3.2-staging
[5]: https://groups.google.com/forum/#!msg/beagleboard/A5Pmw94kFfo/nS9wVMPG4zEJ
[6]: https://github.com/koenkooi/linux/tree/linux-ti33x-psp-3.2.16-r11l+gitr720e07b4c1f687b61b147b31c698cb6816d72f01
[7]: http://designsomething.org/craneboard/w/overview/default.aspx/
[8]: https://github.com/craneboard/craneboard-kernel
[9]: http://www.linaro.org/

