---
layout: post
title: iOS Keep Originals Photo & Video Pain
date: 2020-01-02
comments: false
---

For Christmas I got a new to me iPhone 8.  I'm glad I tried Android but I'm very
happy to be back on iOS.  However, Apple's made a change to how pictures and
videos which the phone takes are stored within iPhones and this causes some
frustration.

The new default, since iOS 11 I think, is to store photos in the HEIC format and
videos in h.265 format.  Prior to iOS 11, JPEG was used for photos and h.264 for
videos.  Most everything can deal with JPEG and h.264 these days but some things
cannot deal with HEIC or h.265.

There's a setting to revert back to using JPEG and h.264 for storage but it's
confusingly named "Most Compatible" within `Settings -> Camera -> Formats` menu
system, and this selects both JPEG and h.264.  There's also a setting for
having the phone convert the HEIC and h.265 files into JPEG and h.264 files on
the fly when you transfer them to a PC called "Automatic" within
`Settings -> Photos` menu, but it's buggy as hell and often results in
"A device attached to the system is not functioning." error messages when
transferring video files to a Windows PC.

My family's Windows 8 laptop has no issue playing h.265 videos but apparently
has no method to deal with HEIC photos, especially not within Picasa which we
use for our photo library.  Hence, JPEG is a hard requirement for us, but h.265
or h.264 are both fine.

Unfortunately, most of my Google results for the "A device attached to the system is
not functioning" error message took me to Apple support forums where the
solution is generally to reboot everything until it works, transferring as much
as you can each time but no one really ever explains what exactly is going on.
And then people who get things working go on to complain that they can't see any
of their photos or that the videos all lack actual video data, just sound plays.
Figuring this all out took me much longer than it should have.

I'm all for newer photo and video encoding schemes if it means I get better
quality and take up less space, but it's not explained what the potential
downsides are anywhere clearly so that people can understand the trade-offs that
are being made for them with the default settings.

I'm happily now setting `Settings -> Camera -> Formats` to "Most Compatible" so
I can just have the file types which I know work well for my needs, even if the
quality is slightly lower and the storage space taken up is slightly higher.
