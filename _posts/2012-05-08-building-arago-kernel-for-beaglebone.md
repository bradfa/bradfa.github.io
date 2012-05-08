---
layout: post
title: Building the Arago Linux Kernel for Beaglebone
date: 2012-05-08
comments: false
---

Things you'll need:

1. The TI [am335x-evm-sdk sources] [1]
2. A git clone of the [Arago am33xx v3.2-staging branch Linux source] [2]
3. Some x86 to [ARM cross compiler (I like Debian)] [3]
4. Patience

First clone the Arago am33xx kernel tree, or if you already have a kernel tree
locally, add the Arago repo as a remote and check out the `v3.2-staging`
branch.  Then unpack the TI am335x-evm-sdk sources, of which you'll then again
need to unpack the Linux kernel sources inside, so that you can get the
Cortex-M3 firmware needed for proper power management.  The firmware is located
at `firmware/am335x-pm-firmware.bin`.  Copy it to the `firmware/` directory in
the Arago kernel tree you've checked out.

Now, within the Arago Linux tree, you'll execute all the rest of the commands.

First, make sure everything's clean:

    make mrproper
    make ARCH=arm clean

Then load the `am335x_evm_defconfig`:

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- am335x_evm_defconfig

If you'd like to make any changes, you may use menuconfig.  I personally like
to enable DEVTMPFS and automatically mount it at boot time since I don't create
any entries in `/dev` on my root file system (I'm lazy, [patch available in
a gist] [4], apply the patch before loading the defconfig):

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- menuconfig

Then build the uImage (replace the -j5 with an apropriate value for your build
machine):

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- -j5 uImage

Copy the resulting uImage to your SD card and boot up your Beaglebone!

    cp arch/arm/boot/uImage /path/to/sdcard/

Make sure when unmounting your SD card that you allow the unmount to return
before physically removing it from your PC.  A `sync` before the `umount`
command is my usual operation, to ensure all data has been written to the SD
card before I pull it.  Linux on your PC will buffer data being written, so the
actual `cp` command will return before data has been fully written to the card.

[1]: http://software-dl.ti.com/dsps/dsps_public_sw/am_bu/sdk/AM335xSDK/latest/index_FDS.html
[2]: http://arago-project.org/git/projects/?p=linux-am33x.git
[3]: http://wiki.debian.org/EmdebianToolchain
[4]: https://gist.github.com/2634388

