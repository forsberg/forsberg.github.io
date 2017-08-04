---
layout: post
title: 'First Impression - Samsung ML-2571N B/W Laser Printer'
tags: [software,hardware,review]
redirect_from: /blog/archive/2006/10/18/first-impression---samsung-ml-2571n-bw-laser-printer
---

Me and my girlfriend ordered a printer a few weeks ago. Today, it
finally arrived.

This is a Black&White Laser printer with network capabilities.

Network Capability
==================

Why network capabilities? Because it's reliable! I'm running a Linux
workstation at home, my girlfriend has a Windows XP box. I don't trust
her machine being up, serving the printer when I need it. She doesn't
trust my machine being up, serving the printer when she needs it. She's
probably right :-). This poor machine is a bit experimental.

So, to avoid any computer-related trouble, we bought a printer with
network connectivuty that could easily be hooked up in our little
apartment-network. The printer speaks 100Mbit/s ethernet and was
configured to get an IP via DHCP at start. Excellent!

Size and Weight
===============

It's a nice little machine. It's very lightweight, so there's no trouble
keeping it on a shelf above the screen. It's also quite small, so there
were no trouble finding a place to put it.

Speed
=====

Very fast! It prints in no time!

Quality
=======

Oh.. well.. it's a black&white printer we'll use for documents, and as
far as I can tell, it prints good enough for that.

Linux Drivers
=============

This is where the, ehm, "fun" begins. I do have quite a lot of
experience in printing on Linux, especially with
[CUPS](http://www.cups.org), so I do have some opinions on how Linux
printers should behave and how to install them.

When it comes to this printer and its Linux drivers, I'm both impressed
and quite unimpressed.

I'm impressed, because there is official Linux support, and not only for
Red Hat Linux 7.3 or some other ancient distribution, but for all kinds
of distributions.

I'm not impressed, because they have missed quite a few things, and the
installation procedure is far from obvious and also full of bugs.

When you insert the CD which claims to contain Linux drivers, you are at
first impressed that they ship a autorun file for Linux. Then you are
less than impressed by the fact that they have missed the fact that many
modern Linux distributions mount CD's noexec. This of course makes the
installation fail ungracefully.

Fortunately, I'm experienced enough to understand this, so after
remounting with exec, I started the installation program
*Linux/install.sh*.

This fires up a QT-based installation program that first tries to locate
a locally connected printer. In my case, it didn't find any such printer
since the printer is connected via the network and not via USB or
parallell port. It then gives the opportunity to search for network
printers. Being curious, I fired up a ethereal to see how it did that,
and found out that it broadcasted for printers using, I think, SLP
(Service Location Protocol). Clever use of standard protocols! It did
find the print after a short while. Impressive!

But after this, I'm unimpressed again. The installation program starts
installing stuff. Yeah, that's right. *Stuff*. It doesn't tell much
about what it's installing, and the manual ain't clear on that either.
Too much magic.

When the installation program ends, I have two processes running as root
doing.. I don't know! The printer has not been added in CUPS. If I try
to print from my web browser, I get a well-designed but malfunctioning
interface featuring a picture with the printer. I don't know how it got
there, and it doesn't work - it tells me the printer is not started.

Oh, my. As usual, hardware manufacturers try to make everything so
seamless and smooth that the result is that nothing works.

Here's my recepy on how printer manufacturers should support printers:

1)  Provide packages for the major Linux distributions with the PPD's
    and any CUPS filters needed.

2)  Provide a installation program that either installs the packages, if
    there is a package for this distribution, or tell the user a number
    of specified files will now be installed at a bunch of specified
    locations.

3)  Let the installation program locate and install the printer in CUPS.

4)  That's all, folks.

I uninstalled the whole thing (there was, and I'm happy and impressed by
this, an *uninstall.sh* shipped on the CD), located the PPD on the CD
and copied it into CUPS' ppd directory, then restarted CUPS and added
the printer via the CUPS web interface. Works as a charm.

