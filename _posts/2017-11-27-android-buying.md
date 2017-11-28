---
layout: post
title: Buying My First Android Phone
date: 2017-11-28
comments: false
---

About a month ago I bought my first Android phone.  I want to document my
reasoning behind why I bought the phone that I did and in time I can review my
decision making and hopefully improve next time I buy a phone.

I had previously used an Apple iPhone 5, my first smartphone (yeah, I know, I
was late to this smartphone party) but with the release of iOS 11, Apple no
longer would support the iPhone 5 with updates of any kind and the phone was
starting to feel very very slow.  I had previously replaced the battery once,
which helped with battery life but there really isn't any way to improve the
phone.  I also simply wanted something newer and more capable, especially a
better camera.

My budget was to keep the purchase price under $300 for a brand new (not
refurbished or used) unlocked (from a carrier perspective) phone with a warranty
and a good camera.  Buying a new phone with a warranty was important to me
because I cannot afford to throw away a few hundred bucks, so if the phone has
any issues then being able to immediately get the manufacturer to fix it for
free is important.  I had bought my iPhone 5 refurbished, but not by
Apple, and the LTE never really worked correctly.  My price point was $300
because that's as high as I could convince my wife to let me go, but having a
reasonable price ceiling was good as it limited my choices so making a decision
was easier.  Buying an unlocked phone was important to me because I've
previously switched carriers a few times in my life and not needing to buy a new
phone in order to make a carrier switch just seems like a reasonable thing to
expect in 2017.  Having a good camera is important to me because I have small
kids and take a lot of pictures/movies of them.

Secondary goals were to get a phone which had expandable flash, an easy to
replace battery, an unlockable bootloader, waterproofing, and support from one
of the 3rd party ROM communities.  All of the secondary goals relate to being
able to keep the phone for a long time without worrying about outgrowing it or
losing software update abilities.

I bought an [LG G5, model RS988][lgg5rs988].  I paid $250 plus tax at B&H Photo
at the end of October 2017.  Overall, I'm pretty happy with my decision.

[lgg5rs988]: http://www.lg.com/us/cell-phones/lg-RS988-Silver-g5-unlocked

The LG G5 is a 2016 flagship phone that was launched in the first quarter of
2016.  It has a Snapdragon 820 SoC (2x Cortex-A7x-like cores and 2x
Cortex-A53-like cores) which is decently powerful, 4 GB of RAM which is still
quite good in late 2017, 32 GB of flash, an SD card slot, and a fairly highly
rated camera for when it was released.  The LG G5 originally came with Android
Marshmallow, was then upgraded to Android Nougat 7.0 in late 2016/early 2017,
and is expected to probably get Android Oreo soon.

The RS988 is carrier unlocked and has good support for the frequencies used by
Verizon, AT&T, and T-Mobile in the USA.  When I first received the phone I used
it on [Ting][ting]'s T-Mobile MVNO network and it worked fine although service
at my house was less than stellar.  I've since switched to [AT&T][att]'s prepaid
service and get very good service at my house but less than stellar service at
work.  My lesson learned here is that mobile phone provider coverage maps lie
and one must actually test each provider's coverage in the areas which matter to
you.  Verizon, based on coworkers' phones, has good coverage at my office but
my company is moving in the spring to a new building so I'll likely stick with
AT&T for now.  I really liked Ting, they have great customer service and decent
prices, but T-Mobile's network is lacking where I live.

The RS988 has an easy to replace battery.  You power off the phone, hold the top
securely in one hand while depressing a small button, and then slide the bottom
of the phone away and the battery comes with it.  Pop the old battery out of the
bottom piece of the phone, insert new battery, and reassemble.  The total
experience is very easy and takes only a minute or two.  I am very excited by
this as in a year or two when the original battery starts to show reduced
capacity I can easily replace it without the use of any tiny screw drivers,
plastic spudgers, or heat guns as are needed on 98% of phones today.

The RS988 has an unlockable bootloader.  [LG has a website][bootloaderunlock]
and an official policy where you can request a bootloader unlock key so that you
can install any software you like onto the phone.  I've requested and received
my bootloader unlock key but I haven't yet actually unlocked the bootloader as
doing so will likely cause Netflix to stop working and possibly not allow me to
receive software updates from LG for the stock ROM.

[bootloaderunlock]: http://developer.lge.com/resource/mobile/RetrieveBootloader.dev

Other LG G5 models have official support from [Lineage OS][lineage] and the
RS988 model is included in the build system for Lineage.  Hopefully this just
means that no one has actually stepped up to take ownership of a Lineage RS988
build but I haven't yet learned enough about AOSP to fully understand this.
Possibly this is an opportunity for me to continue to get software and security
updates for many years once LG drops support.

[lineage]: https://wiki.lineageos.org/devices/

The one downside of buying a carrier unlocked phone that I've learned since
getting my G5 is that the fancy calling features like VoLTE (voice over LTE), HD
Voice (which may simply be VoLTE, I don't really know), and Wi-Fi calling do not
generally work as the carriers block these services from working on
non-carrier-branded phones.  This isn't a huge deal except that if Wi-Fi calling
would have worked for me then I would have been able to stay with Ting as I have
decent enough Wi-Fi at home even with poor T-Mobile coverage so making calls
still would've worked fine.  The VoLTE issue is likely only to present itself in
areas where a carrier only has LTE coverage and no 3G service, which is likely
fairly rare, but is something that T-Mobile is doing now apparently.  I'm unsure
if Apple iPhones which are purchased directly from Apple unlocked have these
features be usable or not.

My transition to Android has gone fairly smoothly, I'm still able to sync my
calendar and contacts from iCloud using [DAVdroid][davdroid], so my wife and I
still can share these while she's still on her iPhone.  I was able to replace
the stock LG launcher which tries very hard to be like iOS, but fails miserably,
with [OpenLauncher][openlauncher] which is pretty simple and works well.  I
tried a bunch of different email clients and have found [K-9 Mail][k9mail] to
work really well for my needs.  And I like that I can use Firefox for web
browsing (I've been a Firefox devotee since shortly after its 1.0 release, and a
Mozilla/Netscape user since I first got on the web).  The G5's camera is pretty
good, I actually really like the wide-angle abilities, although the camera app
is full of features which I don't care about (the selfie cam can fix your
blemishes! For goodness sake...).

[davdroid]: https://www.davdroid.com/
[openlauncher]: https://github.com/OpenLauncherTeam/openlauncher
[k9mail]: https://k9mail.github.io/

The biggest things I miss from iOS are:

* IPP Everywhere (Air Print) printing, it just works on iOS but most printers
  seem to need an app/plugin for Android.
* mDNS name resolution just works everywhere in iOS (and in Linux with Avahi and
  on Windows with Apple's Bonjour) but doesn't seem to be something Android
  offers (although mDNS-SD does work).
* iMessage.  Apple does iMessage very well.  I've yet to find an app like it on
  Android which doesn't provide plain text to Google which is anywhere close to
  iMessage's abilities.
* Timely software/security updates.  My G5 is still on the July 2017 security
  update while my wife's iPhone has gotten multiple security updates that fix
  CVEs since the iOS 11 release in September.  This can be resolved by using
  Lineage OS but I really hope LG does better after Oreo lands.

But for a $250 phone, compared to paying much more for an Apple phone, I went
into this understanding that there'd be trade-offs and changes from iOS and that
likely I'd need to put in some time and effort to get a 3rd party ROM working in
the long run.

Just today, November 28th, 2017, B&H Photo now lists the RS988 model as
discontinued.  There's still a few vendors online who will sell new one but I
expect those will decline fairly quickly now.  The G5 seems to have been a
fairly unloved phone by reviews sites so hopefully the used market will provide
the ability to buy low cost gently used RS988 phones in the near future so that
I can get one cheap to work on Lineage OS with :)
