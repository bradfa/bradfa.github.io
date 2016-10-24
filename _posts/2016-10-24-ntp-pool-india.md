---
layout: post
title: NTP Pool Server in India
date: 2016-10-24
comments: false
---

About a month ago, [LWN ran an article about the NTP pool system][lwn-ntp].
I've been  meaning to learn more about NTP and how the pool system works because
I'd like to be able to setup a vendor zone for my dayjob employer in the near
future and so I figured it was as good a time as any to dive right in!

[lwn-ntp]: https://lwn.net/Articles/701222/

I wanted to setup my server somewhere that it would be hit hard and also provide
services to an underserved part of the world.  India was the only country I
could find where there was a low cost VPS provider and also a dearth of NTP pool
servers...

So, I now run one of the NTP pool servers in India!  You can see my server's
statistics as measured by the pool monitoring station on [my pool user
page][pool user page].  My server is a stratum 2 server, so it tracks the time
from a handful of stratum 1 and other stratum 2 servers.  At peak times my
server is serving almost 1 million clients and doing upwards of 10 Mbps inbound
and outbound network traffic, which I find quite impressive!

[pool user page]: http://www.pool.ntp.org/user/bradfa

My server is hosted on [Digital Ocean][digital ocean] (that's a referral link)
in their BLR1 zone in Bangalore, India on a $5/month droplet, and I'm quite
happy with it.  Currently, Digital Ocean does not actually track network
transfer totals, which is a good thing, as I expect my total monthly transfer
will be in the 2 to 3 TB range.

[digital ocean]: https://m.do.co/c/38c608229292

Although at this point my NTP pool account lists an IPv6 server, it is due to
be removed from the pool in a week or so.  When my server is in the IPv6 pool,
there are times when CPU usage goes extremely high and my server starts to fall
behind in responding to NTP requests but I've not yet been able to debug why
this sometimes happens.  By removing my server from the IPv6 pool, this issue
completely goes away, so at least for the short term, this is my remedy.

It's interesting to watch my network transfer rates, during normal business
hours, there's a steady level of NTP traffic at about 8 Mbps, then around dinner
time it starts rising up to a peak around 10 Mbps, then finally around midnight
it starts to taper off down to a minimum of about 2 Mbps.  This cycle happens
consistently, day to day, and week to week.  I still need to setup local
monitoring and have it produce pretty graphs, I just haven't gotten to that,
yet.

The official ["How do I join pool.ntp.org"][how to join] web page states,
*"Currently most servers get about 5-15 NTP packets per second with spikes a
couple of times a day of 60-120 packets per second. This is roughly equivalent
to 10-15Kbit/sec with spikes of 50-120Kbit/sec."* which might be true for
servers in the west, but is definitely not true for underserved parts of the
world.  I see thousands of packets per second on my server.

[how to join]: http://www.pool.ntp.org/en/join.html

If you'd like to set up an NTP server and have it join the world-wide NTP pool
system, I highly recommend it!  You can find underserved parts of the world to
focus on by drilling down within the [Global region][global] listing.  I've
found that the Africa and Asia regions are not well served, especially India and
China, but both countries have quite large online populations.  India is much
easier to find hosting providers, in my experience, so that's where I focused.

[global]: http://www.pool.ntp.org/zone/@
