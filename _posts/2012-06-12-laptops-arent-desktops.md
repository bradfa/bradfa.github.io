---
layout: post
title: Laptops Aren't Desktops
date: 2012-06-12
comments: false
---

The premise must seem like a stupid statement.  Of course laptops aren't
desktops, why would someone think otherwise?

There's a whole industry out there making laptop computers, many of the
companies making laptops also make desktops.  And there's a class of consumer
who wants the power of a desktop but the portability of a laptop, and they're
apparently not willing to buy 2 computers.

The compromise that this consumer is asking for is being given to the market
by the computer making companies, but it's a horrible compromise, getting none
of the good things from either class of computer.

Let's use the HP Elitebook 8560w as an example.
I happen to have one handy on my desk and
have been using it as my only work computer since December 2011.  I've
[written about it before][1]. I run Debian on it, quite successfully.

My Elitebook has a dual core Intel Core-i7 (with HT, so 4 cores, sort of), 8GB
of RAM, a solid state disk, NVIDIA graphics, and a 24" HP IPS monitor via
DisplayPort.  It's a decent little machine and gets the job done quite well for
me.  But here's the catch, for the same money, I could have gotten a desktop
that would be even faster, have more of the ports I wanted (dual Ethernet, real
serial port, and PCI-e expansion), and had less configuration issues (wifi not
needed on a desktop, and the internal monitor is lower in res than my external
but apparently X doesn't understand that I'm not using the internal monitor so
when I maximize things they don't actually fill the external monitor).  AND!
It's a 15 inch laptop that's almost 1.5 inches
thick and weighs in right around 7 pounds.  To say the least, a MacBook Air
is a dream in comparison (the 11 inch Air is about as thick as just the screen
on the 8560w!).

To fix the lack of dual Ethernet, I have a [Belkin ExpressCard Gigabit Ethernet
card][2], but it's a 34 mm ExpressCard and the 8560w has a 54 mm wide slot, and
since there's no support built into the 8560w for the skinnier cards, if I so
much as move the 8560w slightly, the ExpressCard loses contact and I lose my
second Ethernet port (which no longer causes Linux to lock up hard since I've
enabled PCI hotplug, but is still annoying since the DHCP server goes down and
if I have iptables routing going really pisses off the kernel).

So, I've got a laptop that's not easily portable and a desktop that lacks some
of the speed and ports that I really want.  Never mind that ECC memory or more
than 4 real cores wasn't even an option on the 8560w (it is on many desktops I
would consider buying).

I thought that I only needed one machine. I was wrong.  The 8560w I got is
not stellar at being either role that I want.  The cost was lower than
purchasing two different machines, but not by that much.  And I may not have
even needed a powerful laptop, something portable for $500 would cut the
mustard, especially if I could SSH into my desktop to do "real work".

After having used the 8560w for almost 8 months, I've come to the conclusion
that I won't be buying a "desktop replacement" laptop ever again.  They don't
replace a desktop, and they aren't very portable laptops.  Something like a
MacBook Air and a decent mid-range workstation would make me much happier and
probably more productive.

I will say, though, that since having a solid state disk, I'll never go back
to having spinning platters for any machine that real work gets done on.
No. Way.  Working with the Linux kernel git tree on spinning disks is a good
way to practice patience.  Working with the Linux kernel git tree on a solid
state disk is at least bearable, and not that slow with a hot cache.

[1]: /2011/11/debian-6-amd64-on-hp-elitebook-workstation-8560w
[2]: http://www.amazon.com/gp/product/B000GB0N14/ref=as_li_ss_tl?ie=UTF8&tag=bradford07-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=B000GB0N14

