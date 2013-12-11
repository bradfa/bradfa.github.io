---
layout: post
title: Yubikey NEO Smart Card in Debian
date: 2013-12-10
comments: false
---

I've owned a Yubikey NEO for a while now and I use it every day, both as a PGP
smart card and as just a Yubikey for LastPass.

To get the smart card functionality, you'll need to (just one time) [enable
it][1].  But the not so well documented next thing you'll want to do is to use
your PGP smart card as your SSH key.

*Here's some exact steps!*

On Debian, you'll need to install the "gpgsm" and "gnupg-agent" packages.  Don't
install "monkeysphere".

    sudo apt-get install gpgsm gnupg-agent

Configure gpg to use the agent:

    echo "use-agent" >> ~/.gnupg/gpg.conf

Enable ssh support for gnupg-agent:

    echo "enable-ssh-support" >> ~/.gnupg/gpg-agent.conf

Use the Yubikey udev rules installed to /etc/udev/rules.d/ 70-yubikey.rules
(provided by the [Yubikey personalization][2] sources):

    # Udev rules for letting the console user access the Yubikey USB
    # device node, needed for challenge/response to work correctly.
    
    ACTION=="add|change", SUBSYSTEM=="usb", \
      ATTRS{idVendor}=="1050", ATTRS{idProduct}=="0010|0110|0111", \
      TEST=="/var/run/ConsoleKit/database", \
      RUN+="udev-acl --action=$env{ACTION} --device=$env{DEVNAME}"

Likely you'll want to log out and back in again to have the agent start with the
proper configuration.  Then insert your Yubikey NEO (or other PGP smart card).

Then you can import your identity from the smart card (assuming you have already
setup your smart card) with:

    gpg --card-edit
    fetch
    quit

If that's failing, make sure you've generated all your keys, uploaded the
public portions to a key server, and then updated your smart card so it knows
where to find the public keys on the key server, which should show you a line
like:

    URL of public key : http://pgp.mit.edu:11371/pks/lookup?op=get&search=0xF3B5C4876114BEA6

Check the status of the card once more to make sure everything is in place and
to ensure gpg is good to go:

    gpg --card-status

See that ssh-add will use the card (and my result):

    ssh-add -l
    2048 4a:9b:8b:03:f9:36:91:93:d0:2e:02:f4:3b:4f:23:8c cardno:000000000001 (RSA)

Now ssh into something and you'll get prompted for your PIN and the PGP card
will do your SSH auth for you (look Ma, no more private keys on disk!):

    ssh -v user@example.com

[1]: https://www.yubico.com/2012/12/yubikey-neo-openpgp/
[2]: https://github.com/Yubico/yubikey-personalization/blob/master/70-yubikey.rules
