---
layout: post
title: ArchiTech Hachiko Board UART Sanity Rework Exact Steps
date: 2017-07-14
comments: false
---

I have an ArchiTech Hachiko development board which has a Renesas RZ/A1 ARM SoC
on it.  I'm quite excited about this SoC as it has 10 MB of SRAM inside the
package along with a 400 MHz ARM Cortex-A9 processor, which is enough to easily
run real Linux without requiring any external SDRAM.

Documentation on this board can be found from the vendor:

* http://architechboards-hachiko-tiny.readthedocs.io/en/latest/
* http://downloads.architechboards.com/doc/Hachiko/download.html

The design of the ArchiTech Hachiko board uses an FTDI UART to USB chip with a
mini USB port directly on the board.  Sadly, this FTDI is connected up such that
when you connect a USB cable to the mini USB port that the entire board gets
powered up.  So, if you want to use this FTDI, it's hard to do interesting
development work for very early boot operations of the SoC.

To fix this, we're going to do a little rework of the board so we can use an
external 3.3 V logic level FTDI cable (like you'd buy for BeagleBone Black use)
connected to the J2 header pins for Tx and Rx and we'll find a ground for the
FTDI over on the ARM JTAG header (or anywhere else you can find a ground pin on
the board).

This will let us keep our FTDI UART connection open on a PC while the Hachiko
board is on, off, in reset, or in any other state which might affect the
on-board FTDI chip.

## Step 1: Locate the resistors

On page 9 of the schematic, locate resistors R15 and R17.  We're going to remove
these two.  In the process of the rework, you may find it easier to remove
resistor R16, too as I've done, it won't serving any useful purpose so feel free
to remove it.

<img src="http://bradfa.github.io/images/hachiko/hachiko-uart-sanity-rework-schematic.png" />

Now, grab your Hachiko board and find these resistors.  They're near the USB
type A connector.

<img src="http://bradfa.github.io/images/hachiko/locate-resistors.jpg" />

## Step 2: Remove the resistors

Remove the jumper from the J2 header.

Grab your soldering iron or hot air rework station and pull the R15 and R17 (and
R16 if you desire) resistors off.  Don't worry too much if you damage the FTDI
chip itself in this process.

## Step 3: Add a green (purple) wire

Now, solder down a very short wire between pad 1 of R15 and pad 1 of R17.  Be
sure that your wire does not touch any of the other now-exposed pads.

<img src="http://bradfa.github.io/images/hachiko/rework-complete.jpg" />

## Step 4: Connect up some wires

Connect an orange jumper wire to pin 1 of J2 and a yellow jumper wire to pin 2
of J2.  Connect the other ends of each of these wires to the correspondingly
colored wire on the external 3.3 V logic level FTDI cable.  Then connect a black
ground wire to pin 20 on header CN1 (the ARM JTAG header) and to the black wire
on the external FTDI cable.

<img src="http://bradfa.github.io/images/hachiko/connect-ftdi-wires.jpg" />

<img src="http://bradfa.github.io/images/hachiko/ftdi-header-colors-lineup.jpg" />

## Step 5: Connect FTDI cable to PC and open your favorite terminal program!

You should now be able to interface with the Hachiko board in your favorite UART
terminal program!

The default code that comes loaded in the QSPI flash on the board uses UART
settings of 115200 8N1, like most all Linux based boards use these days.
