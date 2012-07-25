---
layout: post
title: Next Computer
date: 2012-07-25
comments: false
---

I wrote about how [laptops aren't desktops][1] last month.  I was upset that I
use a laptop that's not very portable but not as powerful as a desktop.  It's
the worst of both worlds.  I still feel that way, but I'm changing my stance on
buying a desktop.

[1]: /2012/06/laptops-arent-desktops

My next computing system won't involve a desktop, per se.  It'll just be a
laptop, and a rather portable one, at that.  It'll also probably be a Mac.
Here's why:

The MacBook Air 13 inch can be specified rather nicely to accomplish 80% of the
things I want to do, for a reasonable price.  The MacBook Pro with Retina
display is a bit more money, can accomplish 85% of the things I want to do, but
is still rather reasonably priced for the hardware.  Either way, I'd get the 27
inch Thunderbolt display to use as a monitor when I'm in "the office."

The only non-Apple laptop I'd consider buying, really, is a Lenovo Thinkpad T
series 14 inch.  And there, a well specified unit could probably accomplish 90%
of what I want to do, but I'd run Linux on it and I'd be frustrated more often.
The extra 5 to 10% improvement of doing the things I want to do may not be worth
the frustrations.

But here's my big change, I wouldn't buy a desktop.  Not today.

In order to get the type of desktop that I want, with the processing performance
I want (because, let's be honest, USB really is good enough for most peripheral
things now and I don't really really need a second Gigabit Ethernet interface, a
slow second Ethernet interface would be good enough), I'd need to spend $4 to
$5k.  I'm not willing to do that.  Not today.

I'd rather invest that $4 to $5k into learning about Amazon EC2 and paying for
time on a [Quadruple Extra Large High-I/O instance][2].  It's only $3.10 per
hour for an 8 core (plus HT), 60 GB of RAM, two 1 TB solid state disks, and 10
Gigabit Ethernet machine.  Damn!

[2]: https://aws.amazon.com/ec2/instance-types/

I'm only going to need really high performance for a few tasks, maybe 2 hours
per day, on average.  That means my costs, per day, would only be something like
$7.  Even with 250 working days per year, my yearly cost would come out to under
$2k.  And, I bet, a decent amount of the things I'd want to do could run almost
as fast on a slightly lower priced EC2 instance.  And, Amazon probably will come
out with new instance types that are either higher performance or lower priced
that I could use, too.

It's hard to connect peripherals to an EC2 instance, but that'd probably  be
OK.  I usually don't need both random peripherals and high compute power at the
same time.

Nothing stops me from trying this idea out now.  Even with a huge laptop, I
could still leverage EC2 for some tasks and start my learning.  I think that's a
good idea.

