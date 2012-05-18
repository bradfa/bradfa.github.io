---
layout: post
title: Why Mainline Matters
date: 2012-05-18
comments: false
---

Yesterday, I wrote a rant about why [it shouldn't take a team][1] of engineers
to buy a dev kit and get mainline Linux running.  A great discussion ensued on
Google+, which was a great reason for me to log into Google+ for the first time
in 3 months, but that's another story...

Mainline matters.  Full stop.

Mainline matters because the people who have to approve patches or pulls in
order for code to make it into mainline are smarter than you.  They're smarter
than me.  They're smarter than most engineers at every ARM SoC vendor.
The people who need to approve code in order for it to make mainline bleed this
stuff, they've been around for decades, hacking Linux.  They've seen almost
all of the tricks in the book.  They will tell you when your code does stupid
things.  Your code will do stupid things.

If I run TI's kernel (that happens to be hosted on Arago, thanks for the
correction) and I run into a problem, how to I send a patch?  How do I share my
problem with others who are running that kernel?  How do I know it gets fixed
correctly?  If I fix it myself, how do I know I'm not doing something stupid
that was tried 5 years ago and failed miserably?

Short answer, I don't.  I'm trusting TI and myself.  TI's great, but they make mistakes
and without the huge amount of experience that exists on mainline mailing
lists taking a look at the code, I don't have huge faith.  Look through a TI
repo, read all the "fixes foo" followed by "actually fixes foo" followed by
"fixes foo again for special case bar" (modified comment from Koen) commits.

I'm putting out a product.  My value add is the software that runs on top of
Linux and the interfaces to the devices outside the SoC.  I want my value adding
to stay at those levels.  If I'm adding value to my company by making Linux
work enough that I can do these other tasks, that's a failure of the
market.  I don't want to worry about the Linux kernel core functionality.

I'm running Debian on my Beaglebones.  I use an old compiler.  Both for the
same exact reason:

**My value add isn't core Linux, it's everything on top and around the core.**

[1]: /2012/05/it-shouldnt-take-a-team

