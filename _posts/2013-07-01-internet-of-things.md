---
layout: post
title: Internet of Things!
date: 2013-07-01
comments: false
---

The Internet of Things gets in the news these days, which is nice.  But we're
still a ways away from where it gets really interesting, mostly due to cost.

Sure, you can buy a refrigerator that connects to the Internet (don't ask why
you would want such a thing, no one knows yet, but that's the beauty).  You can
get a telephone that does so, too.  Heck, I'm sure someone's even made a lock
for your front door that lets people in via the web... [Oh, wait...][1].

[1]:https://lockitron.com/preorder

But most of these "things" that connect to the Internet today use Wi-Fi and
Wi-Fi is a horribly expensive way to connect to a network for "things."

Wi-Fi implies quite powerful hardware, both from a true power consumption point
of view and from a software stack point of view.  Even things like Zigbee or
802.15.4/6LoWPAN require quite decent hardware specs (IPv6 has been said to
require at least 16 kB of RAM to function well, afaik).  This means not only are
rather large batteries required, many times also needing recharging, but the
minimal hardware to attach to such a network needs at least $3 of hardware.

Antenna, PCB, match network, transceiver, micro, and battery.  If you can do
that, and get decent battery life, for less than $3 in volume, you're doing
quite well.  I'm not saying it's not possible, just very very difficult with
today's parts.

Hence, I think the really interesting Internet of Things applications happens
when the cost gets below $1 to manufacture.  We're probably not that far away
from it but I don't think Wi-Fi or 6LoWPAN as specified today will be how we get
there.  The really interesting uses of an Internet of Things is when everything
has access to the net, and that won't happen with commodity items till the extra
cost to buy an Internet enabled device is almost non-existent compared to the
non-Internet enabled device.

Take for instance, my toaster.  It's not Internet connected and really all I
want it to do is to toast things.  But if I'm going to spend $30 on a new
toaster, a 10% increase to $33 (see above for costs) seems silly to me, what
exactly does my toaster need the net for?  But if the increase in cost is closer
to $0.50 then why not?  Maybe I can do some neat little project with it or
something.

Toasters are a good judge of cost, I think for this.

But to get the net into all these inexpensive things we need a different
physical layer than is available today.  I think it'll look a lot more like
passive RFID than an active radio.  The need for a power source is very limiting
for many things but passive RFID doesn't need one.  Passive RFID often is
available with "battery assist" in order to increase range, which takes care of
RFID's often cited limited range (think 30+ meters with battery assist).

The cost of passive RFID is cheap, lots of tags are available for < $1.  Often
these tags have no microprocessor but low power micro designs are getting to the
point where they can consume tiny amounts of power and do useful things, which
will be a requirement in order to harvest RF and run.  Some of the new memory
technologies, like FRAM, might help here too in order to boot fast and persist
RAM.

Obviously IPv6 will be the middle layer for this new tech, hopefully not
consuming 16 kB of RAM, and we'll need cheap (think < $50) access points like
our Wi-Fi has today, for any place where these devices want to get online.  But
the real hard part is standardizing this stuff and finding a way to get decent
data rates and functionality for < $1 per thing.

I give it 2 years till we see something like this start to emerge.  6LoWPAN and
Zigbee and 802.15.4 are leading the way today but they will soon be surpassed by
a new generation of very low cost batteryless (and battery assisted) passive
"things" that are net connected.

It'll be fun to watch RFID make this transformation.
