---
layout: post
title: Lock Screen on Suspend via systemd
date: 2020-08-18
comments: false
---

I use xscreensaver to lock my screen after a timeout or by key command from
within the awesome window manager.  I also like to have my screen lock when I
suspend my laptop by closing the lid.

Since systemd now handles detecting lid closure and initiating the suspend, we
can tell systemd to have xscreensaver lock the screen before doing that, too.

Create a file at `/etc/systemd/system/xscreensaver_suspend@.service` with
contents like:

```
[Unit]
Description=xscreensaver suspend lock service
Before=sleep.target

[Service]
User=%I
Type=oneshot
Environment=DISPLAY=:0.0
ExecStart=/usr/bin/xscreensaver-command -lock

[Install]
WantedBy=sleep.target
```

Then enable this for your user (my user is "andrew") as your user, you don't
need to be root or use sudo, like:

```
$ systemctl enable xscreensaver_suspend@andrew.service
```

Now when you suspend your laptop, xscreensaver should lock the screen first.  If
you have xscreensaver set to fade the screen, the fading action may not complete
until after you resume your laptop, so you screen's contents at suspend time may
be visible for a second or two upon resume.  If this matters to you, disable
fading in xscreensaver-demo interface.
