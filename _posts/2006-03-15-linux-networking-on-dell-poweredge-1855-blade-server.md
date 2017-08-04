---
layout: post
title: 'Linux Networking on Dell Poweredge 1855 (blade server)'
tags: [general]
redirect_from: /blog/archive/2006/03/15/linux-networking-on-dell-poweredge-1855-blade-server
---

A few days ago I visited a customer, installing Fedora Core 4 on a Dell
Poweredge 1855, a blade server. This proved to be rather difficult when
it came to network connectivity.

The Linux kernel recognized two Intel e1000 interfaces, but did not
detect any link. Also, ethtool's list of supported ports only includes
"FIBRE", which was kind of wrong. At least one of the ports should be
"TP".

We fiddled around for a while upgrading the kernel and trying various
versions of the e1000 driver, with no success. We gave up, wrote some
mail to the people at Intel, connected the server with a USB network
card and did what we were there to do - although we had to visit the
server once every 30 minutes or so because the USB network card ceased
to function now and then. Oh well, 3com..

Anyway, the day after we got a response from Intel. It turned out that
if you connected the server to a Gigabit port in a switch, and locked
that port to Full Duplex, the card began to work. Hooray!

Note: I won't take false credit for the solution to this problem. My
colleage [Pierre Ossman](http://drzeus.cx/) did most of the hard work.

