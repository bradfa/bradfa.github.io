---
layout: post
title: Iterate Hardware Like Software
date: 2012-03-05
comments: false
---

Engineering companies don't iterate on hardware like they do with software.
This is a **BAD THING!**

Software is developed in iterations (agile, lean, and a million other buzz
words made up every year).  Write some code, compile, run, test, repeat.  When
it's good enough, ship it.  Continue iterating to add features and squash bugs.
Job done.  That's software.

Hardware is developed with a mindset that, "It sure as hell better work the
first time!"  This is wrong on so many levels.  It takes a heck of a lot longer
to make something work on the first try, so the engineer becomes very risk averse.
Anything that might not work gets outrageous attention, which takes time.

Even simple things get reviewed once, twice, three times, and by a committee.
There's schematic reviews, layout reviews, and BOM reviews.  All have to be
attended by a huge number of people.  God forbid one little thing is wrong,
because then **IT WON'T WORK AND THE SKY WILL FALL AND OUR FIRST PROTOTYPE
WON'T BE LOVED BY ITS MOMMY!**

**NO!**  This is wrong!

Iterate on hardware like your software team iterates on software.  Constantly.
Build early, build often, fail constantly!  It's only through failure that the
weaknesses are found and can be removed.  If the first prototype shows up and
it doesn't work at all, find out why, fix it (physically if possible) and update
the design documents.  Then build another.  Find its failings, fix them.  And
repeat.  When a prototype works well enough, **SELL IT!**  Then keep iterating
to make it cheaper, easier to manufacture, etc, all of which **MAKE MORE MONEY!**

In complete tandem to this, if your hardware has software or firmware that's
expected to run on it (let's be honest, it does, everything does), your
software team can't figure out if their software works until the hardware
arrives.  If, when the hardware arrives, it's different than the software team
thought, there's a huge effort to correct things in the software.  This may
take weeks.  You don't want that.

If you have hardware prototypes showing up every week, in various states of 
working-ness, the software people can start trying stuff out.  They'll even be
able to work around some of the hardware bugs with their code, getting you to
a sellable product even faster.  There won't be any week or month long project
for the software team because the hardware works differently than they expected,
they'll be involved the entire time though the hardware's development.

And!  Once the hardware is "good enough," your software will likely be as well.
Then you can **SHIP IT AND MAKE MONEY!** which is why we're all here in
the first place.

You should expect that the hardware design files on the hardware engineer's 
computer will be at least 1 or 2 versions newer than the hardware that the
software team is working with.  Every week, new prototypes should be arriving.
Every week, incremental gains can be had in the hardware design.  Every week
you **will be paying for new prototypes**, but only a hand full.
If a feature doesn't make it into a prototype build, **THAT'S OK**
because it will make it in the next build, which is only 1 week away.

Oh yeah, and your contract manufacturing house will already have 90% of the
parts you need on-hand once your first prototype is built, which saves you
even more time for each successive iteration.  Making the leap to designing
hardware this way is hard, it's different, and that first time, you will order
thousands of dollars of boards that **won't work**.  But that's the point!
The next batch you order, in 1 week, **WILL WORK** and your software team will
start coding on them, directly, getting you ever closer to a product you can
sell.

Apple does this with their hardware.  Why don't you?
