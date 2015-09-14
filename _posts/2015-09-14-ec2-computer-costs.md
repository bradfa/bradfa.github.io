---
layout: post
title: EC2 Computer Costs
date: 2015-09-14
comments: false
---

I've [previously written][1] about not buying another desktop computer but
instead simply getting a nice portable laptop and monitor setup and then using
Amazon's cloud computers for computation.  So I figured I should actually try
that and see what it's like.

[1]: http://www.bradfordembedded.com/2012/07/next-computer/

I did a little research on price points and how AWS's EC2 actually works then
tried out a compiling work-load, since most modern laptops can do every other
task with ease, except big compiles, it's really the only use-case that makes
sense for me.  My test case was to build the Yocto Project's Poky
"core-image-minimal" targeting the Beagle Bone.

Building Poky is just a huge set of compiling, first a bunch of tools for the
host machine, and then a root file system and Linux kernel for a target (in this
case the Beagle Bone), so I felt it was a good example to show how much it will
cost to get the computation of a modern workstation when using AWS's EC2.  All
my tests were run with the "fido" release of Poky and do not include performing
the fetching of software packages (as this might be very network dependent and
not very consistent).

Here's my findings:

My day job workstation is an *Intel Xeon E3-1270v3* based machine and it can
build the "fido" release of Poky for Beagle Bone in about *32 minutes* (not
including fetching all the downloads).  I don't consider this to be "fast" but
it's certainly not slow for a modern workstation, but this is my reference as
it's the fastest machine I use and buying one is somewhere in the $1500 range.

My personal laptop is an *Intel Core2Duo* based machine running at a screaming
1.7 GHz which was donated to me by my sister a few years ago after she finished
using it as her college laptop.  It was a nice little laptop when new and still
runs fine, so it works great for me as it was free.  It takes *226 minutes* to
build Poky, which is basically unusable.

I then configured a Debian Wheezy (old stable now) HVM EBS root backed (64 GB of
SSD gp2 EBS volume) instance on EC2 and ran it with various EC2 instance types
to compile Poky.  In total, I believe my full AWS costs for this experiment were
in the $1.60 range, so quite affordable to tryout a few workstations :)

On a *t2.micro* instance which has *1 shared CPU* and costs *$0.013/hour*, I
stopped the build after *559 minutes* because it wasn't even half way complete
and I found that AWS will allow full usage of the CPU for a short while but then
throttle it to only allow up to 10% usage.  For doing normal things like
fetching software or serving up a simple blog, this wouldn't be a bad choice,
but it's not even an old laptop replacement in terms of computation.

On an *m4.large* instance which has *2 CPUs* and costs *$0.126/hour*, I built
Poky for Beagle Bone in *136 minutes*.  This is definitely faster than my laptop
but is not a modern workstation.

On a *c4.xlarge* instance (which uses Intel Xeon E5-2660v3 CPUs) which has *4
CPUs* and costs *$0.22/hour*, I built Poky for Beagle Bone in *59 minutes*.

On a *c4.2xlarge* instance (again, E5-2660v3 based) which has *8 CPUs* and costs
*$0.441/hour*, I built Poky for Beagle Bone in *33 minutes*.  I however did find
that the "8 CPU" are likely actually only 4 CPU and then 4 HT cores, so it's not
"really 8 CPU" but more like 4 with HT.

In conclusion, it seems like if you want a modern workstation on AWS EC2, you're
going to pay at least $0.441 per hour of usage, plus EBS fees (SSD gp2 costs
$0.10/GB*month, so my 64 GB SSD gp2 EBS disk would have cost me $6.40/month).
If you were to step up to a c4.4xlarge instance at $0.882/hour and use a
slightly larger EBS SSD disk, I think you'd have quite a nice "workstation".  I
didn't find EBS's gp2 SSD disks to be slow at all, although my understanding is
that a larger disk gets you more guaranteed IOPs and burst IOPs, so going
slightly bigger is probably better, as the cost is not that much compared to the
EC2 instance costs for decent processing power.

If I was working as someone who could charge an hourly rate and compiling was a
bottleneck for me, I would definitely consider using EC2 for some compiling
work-loads rather than buying a new Xeon E5 workstation.  Scaling the CPU power
up and down is easy and if you don't need to shell out a few thousand dollars up
front to buy a workstation, spending $0.882/hour (or even stepping up to the
c4.8xlarge at $1.763/hour) could easily be justified for a few hours per day of
usage while still staying "reasonable" in cost.

The one annoying thing I found to using EC2 this way was that every time I
launched an instance, I got a new public IP address, so using my own DNS was not
possible and my ssh known keys file filled quickly with crap.  Amazon offer a
service to avoid this, where you reserve a public IP address for your own use,
but you pay $0.005/hour of time where this IP is not bound to a running
instance.  So basically it's roughly $3.50/month to reserve an IP address.  If I
was actually using EC2 for work, I'd definitely do this to keep a sane IP
address setup.

Overall, I now understand AWS EC2 slightly better and would highly recommend
using it if you have a need for high compute power.  It's not as convenient as
having a workstation in your office, but it can be a reasonably priced way to
get compiling done.
