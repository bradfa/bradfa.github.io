---
layout: post
title: Flashbenching
date: 2014-05-07
comments: false
---

I'm co-mentoring a Google Summer of Code project this year which is focused on
the MMC and SD subsystems specifically for TI's AM335x but more generally for
all device types which interface to MMC and SD cards.  The goal is to improve
the performance as much as possible within the Linux kernel for these types of
"disks".

Flashbench will be used, at least somewhat, for benchmarking SD card
performance.  Arnd wrote a great overview of managed flash memory, flashbench,
and how using cheap SD cards like a disk is both good and bad on [LWN][-2] a
while back.  You can grab the source for flashbench from either [my github][-1]
or from [Arnd's Linaro git][0] repo.  My repo's "dev" branch has a few small
fixes which are not "upstream" in Arnd's repo.

So, here's a quick little run down of important things to capture
with flashbench.  These tests are running on a white BeagleBone which has an
external SD card interface wired up to it.  Similar tests can be done with a
BeagleBone Black when booting from eMMC so that tests can be run on the microSD
card in the slot.

In this post, I'll test the [Kingston 4GB microSDHC][1] card which used to ship
with BeagleBones.  Don't worry, I've already sent [the results][new] to the
[flashbench-results mailing list][3] (as should you if you test cards with
flashbench).

[-2]:http://lwn.net/Articles/428584/
[-1]:https://github.com/bradfa/flashbench/tree/dev
[0]:http://git.linaro.org/people/arnd.bergmann/flashbench.git
[1]:http://www.kingston.com/us/flash/microsd_cards#sdc4
[3]:http://lists.linaro.org/mailman/listinfo/flashbench-results
[new]:http://lists.linaro.org/pipermail/flashbench-results/2014-May/000475.html

Grab the info which Linux finds about the Kingston card, and pay attention to
the "name" and "oemid".  The "oemid" often will indicate who has made the
controller within the SD card itself (it's hex for ASCII, here 0x544d means
"TM").

````
root@localhost:~# head /sys/block/mmcblk1/device/* 2>/dev/null | grep -v ^$
==> /sys/block/mmcblk1/device/block <==
==> /sys/block/mmcblk1/device/cid <==
02544d5341303447113533890900d371
==> /sys/block/mmcblk1/device/csd <==
400e00325b5900001d177f800a40008d
==> /sys/block/mmcblk1/device/date <==
03/2013
==> /sys/block/mmcblk1/device/driver <==
==> /sys/block/mmcblk1/device/erase_size <==
512
==> /sys/block/mmcblk1/device/fwrev <==
0x1
==> /sys/block/mmcblk1/device/hwrev <==
0x1
==> /sys/block/mmcblk1/device/manfid <==
0x000002
==> /sys/block/mmcblk1/device/name <==
SA04G
==> /sys/block/mmcblk1/device/oemid <==
0x544d
==> /sys/block/mmcblk1/device/power <==
==> /sys/block/mmcblk1/device/preferred_erase_size <==
4194304
==> /sys/block/mmcblk1/device/scr <==
0235800001000000
==> /sys/block/mmcblk1/device/serial <==
0x35338909
==> /sys/block/mmcblk1/device/subsystem <==
==> /sys/block/mmcblk1/device/type <==
SD
==> /sys/block/mmcblk1/device/uevent <==
DRIVER=mmcblk
MMC_TYPE=SD
MMC_NAME=SA04G
MODALIAS=mmc:block
````

Get what the actual size, in bytes, the card is by using fdisk.  This can often
help to indicate the eraseblock size.  You can factor this number to see what
the prime factors are, often indicating if a power of 2 number of bytes are
likely in the eraseblock size.

````
root@localhost:~/flashbench# fdisk -l /dev/mmcblk1

Disk /dev/mmcblk1: 3904 MB, 3904897024 bytes
4 heads, 16 sectors/track, 119168 cylinders
Units = cylinders of 64 * 512 = 32768 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00000000

Disk /dev/mmcblk1 doesn't contain a valid partition table

root@localhost:~/flashbench# factor 3904897024
3904897024: 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 7 7 19
````

Then we can run the "read" performance test.  This often can indicate where
eraseblock bounds are, where one erase block ends and the next begins.  This is
important as each eraseblock must be erased all at once (it's how flash works)
and so if you, for instance, want to change just one bit within an eraseblock
the controller will often copy the entire eraseblock contents to another
eraseblock but with your one bit change.  The controller will then set the old
eraseblock to be erased, possibly in the background.  Knowing how big each
eraseblock is can be used to align your partitioning scheme with the underlying
media, to improve performance.

This is just a non-destructive read test.  Sometimes read performance when
spanning two eraseblocks will be slower than when reading only in one erase
block.  The "pre" reads just prior to an expected eraseblock boundary, the "on"
reads spanning an eraseblock boundary, and the "post" reads just after an
eraseblock boundary.  Any spot where the "diff" times drop dramatically may
indicate the likely eraseblock size or the likely write page size (write page
size will always be smaller than an eraseblock).

````
root@localhost:~/flashbench# ./flashbench -a /dev/mmcblk1 --blocksize=1024
align 1073741824	pre 1.77ms	on 2.4ms	post 1.66ms	diff 686µs
align 536870912	pre 1.72ms	on 2.36ms	post 1.64ms	diff 684µs
align 268435456	pre 1.75ms	on 2.39ms	post 1.64ms	diff 696µs
align 134217728	pre 1.75ms	on 2.35ms	post 1.62ms	diff 667µs
align 67108864	pre 1.74ms	on 2.37ms	post 1.62ms	diff 695µs
align 33554432	pre 1.75ms	on 2.37ms	post 1.62ms	diff 682µs
align 16777216	pre 1.74ms	on 2.37ms	post 1.63ms	diff 681µs
align 8388608	pre 1.72ms	on 2.33ms	post 1.62ms	diff 658µs
align 4194304	pre 1.66ms	on 2.27ms	post 1.58ms	diff 650µs
align 2097152	pre 1.55ms	on 2.19ms	post 1.63ms	diff 605µs
align 1048576	pre 1.6ms	on 2.21ms	post 1.66ms	diff 576µs
align 524288	pre 1.61ms	on 2.21ms	post 1.65ms	diff 581µs
align 262144	pre 1.6ms	on 2.2ms	post 1.65ms	diff 576µs
align 131072	pre 1.61ms	on 2.2ms	post 1.64ms	diff 580µs
align 65536	pre 1.56ms	on 2.16ms	post 1.62ms	diff 566µs
align 32768	pre 1.56ms	on 2.09ms	post 1.61ms	diff 504µs
align 16384	pre 1.53ms	on 2.11ms	post 1.59ms	diff 544µs
align 8192	pre 1.67ms	on 1.67ms	post 1.64ms	diff 19µs
align 4096	pre 1.72ms	on 1.74ms	post 1.73ms	diff 14.6µs
align 2048	pre 1.75ms	on 1.76ms	post 1.76ms	diff 11.8µs
````

Possibly this Kingston card has 2 or 4 MiB eraseblocks but it's not that clear.
The drop from 4 MiB to 2 MiB and again from 2 MiB to 1 MiB mean the eraseblock
is probably 2 or 4 MiB.  We'll assume it's 4 MiB for now.

Next, run some "open-au" tests.  An "open-au" (open allocation unit) test will
tell how many of those copy-on-write-then-erase (aka: garbage collection)
operations I mentioned above can happen simultaneously.  Cheap controllers can't
handle more than 1 at a time while high end controllers can sometimes do 30 or
more.  Any card which can handle 5 or more "open-au" is quite good.

The "open-au" tests will write, in various sizes down to the blocksize you
specify, to a sequence of eraseblocks.  If the controller is able to sustain
more than 1 "open-au" then when running with 2 "open-au" the performance should
be about the same as with 1 "open-au".

````

root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --open-au-nr=1
4MiB    6.45M/s 
2MiB    5.19M/s 
1MiB    5.19M/s 
512KiB  5.1M/s  
256KiB  5.15M/s 
128KiB  5.14M/s 
64KiB   5.1M/s  
32KiB   4.94M/s 
16KiB   3.71M/s 
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --open-au-nr=2
4MiB    3.88M/s 
2MiB    5.19M/s 
1MiB    5.12M/s 
512KiB  5.06M/s 
256KiB  4.99M/s 
128KiB  4.77M/s 
64KiB   4.64M/s 
32KiB   4.53M/s 
16KiB   3.38M/s 
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --open-au-nr=3
4MiB    4.47M/s 
2MiB    5.19M/s 
1MiB    5.17M/s 
512KiB  5.12M/s 
256KiB  4.96M/s 
128KiB  4.77M/s 
64KiB   4.65M/s 
32KiB   4.49M/s 
16KiB   3.36M/s 
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --open-au-nr=4
4MiB    6.06M/s 
2MiB    4.49M/s 
1MiB    2.82M/s 
512KiB  1.25M/s 
256KiB  607K/s  
128KiB  302K/s  
^C
````

I've stopped the "open-au" test with CTRL-C as it will take a very very long
time to complete once the card gets slow.  Here we can clearly see that 3
open-au have good performance, while 4 is a dog.

Now for the random version of the "open-au" test where instead of writing the
eraseblocks in sequence, they are written "randomly" to stress the controller
dealing with writes out of order.  For good performance with a file system, you
want this test to show at least 3 "open-au" and reasonable M/s numbers.

````
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --random --open-au-nr=1
4MiB    3.07M/s 
2MiB    2.13M/s 
1MiB    3.24M/s 
512KiB  1.44M/s 
256KiB  1.76M/s 
128KiB  1.91M/s 
64KiB   1.36M/s 
32KiB   1.18M/s 
16KiB   1.2M/s  
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --random --open-au-nr=2
4MiB    3.03M/s 
2MiB    2.58M/s 
1MiB    3.26M/s 
512KiB  1.44M/s 
256KiB  1.75M/s 
128KiB  1.9M/s  
64KiB   1.36M/s 
32KiB   1.17M/s 
16KiB   1.18M/s 
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --random --open-au-nr=3
4MiB    3.03M/s 
2MiB    2.78M/s 
1MiB    3.25M/s 
512KiB  1.44M/s 
256KiB  1.76M/s 
128KiB  1.9M/s  
64KiB   1.36M/s 
32KiB   1.18M/s 
16KiB   1.19M/s 
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --open-au --erasesize=$[4*1024*1024] --blocksize=$[16*1024] --random --open-au-nr=4
4MiB    3.33M/s 
2MiB    2.92M/s 
1MiB    2.48M/s 
512KiB  1.2M/s  
256KiB  595K/s  
128KiB  298K/s  
64KiB   150K/s  
^C
````

This Kingston card is definitely no speed demon but it isn't quite as bad as the
[older Kingston card of the same model number][old] I tested 2 years ago.  That
there's variability within the same model number card is not something you want
to see, as a customer, since results will vary even though you can't physically
tell the cards apart.

[old]:http://lists.linaro.org/pipermail/flashbench-results/2012-February/000252.html

Lastly, we can check if the first few eraseblocks have any special ability.
Some cards will provide for the first few eraseblocks to be backed by SLC flash
instead of MLC, or otherwise improve the performance of these special
eraseblocks.  This is important when using the card with the FAT filesystem as
all the metadata is stored in the beginning of the disk and will get the most
wear and small writes.

````
root@localhost:~/flashbench# ./flashbench /dev/mmcblk1 --find-fat --erasesize=$[4*1024*1024]
4MiB    865K/s   3.56M/s  3.01M/s  5.13M/s  5.14M/s  5.12M/s  
2MiB    4.3M/s   4.88M/s  5.11M/s  5.16M/s  5.11M/s  5.3M/s   
1MiB    3.99M/s  4.9M/s   5.23M/s  5.18M/s  5.17M/s  5.15M/s  
512KiB  3.88M/s  4.81M/s  5.15M/s  5.16M/s  5.16M/s  5.15M/s  
256KiB  4.35M/s  4.38M/s  5.17M/s  5.18M/s  5.17M/s  5.16M/s  
128KiB  3.78M/s  4.8M/s   5.13M/s  5.12M/s  5.15M/s  5.14M/s  
64KiB   4.27M/s  4.74M/s  5.08M/s  5.03M/s  5.08M/s  5.07M/s  
32KiB   3.62M/s  4.29M/s  4.97M/s  4.96M/s  4.96M/s  4.95M/s  
16KiB   3.01M/s  3.31M/s  3.74M/s  4.29M/s  4.3M/s   4.29M/s 
````

There doesn't appear to be any special FAT area in this Kingston card.

In summary, this card is not so hot.  But then again, it was bundled with a
BeagleBone and so price was likely much higher concern for the seller than
performance.
