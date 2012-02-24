---
layout: post
title: Smells Like Electrolytic Capacitors
date: 2012-02-24
comments: false
---

Waking up at 2 am yesterday morning, I smelled something funny.  My house was
not burning down, which was good, but something didn't smell right.

Opening the door to my home office, the smell got much, much worse.

My wife had been using the office that day and had left her laptop on the desk.
It was still on and so became the prime suspect in my search for the smell
generator.  We shut everything down, pulled all the power cords for all devices
in the office out of their
outlets, opened the windows (it was about 30 degrees F outside, thankfully not
any colder), and started to air out the room.  Airing out lasted about an hour
before we both were fed up waiting, but the smell had reduced to a much lower
level and still nothing was on fire, so we closed everything up, put her laptop in
another room and went back to sleep.

If the laptop was the root of the smell, the smell should follow it.  The smell
did not follow it.

So that left my desktop computer...

I didn't have time to investigate in the morning, but the smell was not as bad
as it was in the middle of the night.  Keeping the door and all heating vents
in the room closed, I went off to work.  Upon my return, yesterday evening, the
smell was still present, but at a reduced level.  Since I was now awake (2 am
isn't my brain's best hour), I tried powering on my desktop.

No dice.  My raid card usually beeps every time the PCI bus reset gets pulled
(which happens twice at normal power up), it made the most sad sound a RAID card
with a buzzer can make.  Like it had lost its soul.  And then no boot.  So, 
seeing as the machine wouldn't boot, the first thing that came to mind was
either the power supply or motherboard.

A quick bit of looking at my desktop's motherboard showed no signs of dying
electrolytic capacitors or other obvious signs of death, so the power supply
became the prime suspect.  Pulling the power supply and looking closely though
the fan grates yielded the culprit: electrolytic capacitors with their
electrolyte popping out of the top of the can...  That's not good...

The power supply has since been relegated to the garage, to wait until the next
time I recycle some electronics.  I'm now waiting patiently for the UPS guy to
show up with a new Seasonic 520 Watt unit.  It can't come fast enough! :)

Last year, about this time, I was experiencing some RAM troubles.  When ever
I would plug in an SD card reader, the kernel would complain about ECC errors.
If I let it go long enough, I'd get to enjoy a fun crash.  Performing a bunch
of memory tests yielded no errors when running memtest86+.  Regardless, every
time I plugged that SD card reader in, ECC errors would arise and shortly
thereafter, a crash.  I narrowed the errors down to 4 of my 8 sticks of DDR
memory, after removing them, the ECC errors and crashes went away.

I suspect that the power supply had been dying for quite a while, and that it
may have actually been the root cause of my ECC errors.  Since memtest86+
could not detect any problems, even when run for a full day, things just weren't
adding up.  Maybe I'll get to reinstall the other half of my DDR once the new
power supply arrives, that'd be a nice bonus.

If you're wondering why I didn't just buy new DDR, you should price out
registered ECC DDR400.  It's not cheap, but I am.  One 1GB stick from Crucial
costs as much as the power supply I just bought.  My desktop is a 5+ year old dual
processor (physical ones, not cores) AMD Opteron box, and memory must be
installed equally between the two processors and in pairs (to get dual-channel
operation), so the only choices are 4 or 8 sticks of DDR if I want reasonably
good performance.  I was too cheap to try and buy another stick of DDR since
my computer still worked and the impact of half as much memory really wasn't
that bad.  Although the prospect of getting it all back would be nice...
