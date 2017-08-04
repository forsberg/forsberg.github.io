---
layout: post
title: 'Squeezecenter Performance on QNAP TS-109 II'
tags: [turbostation,squeezebox]
redirect_from: /blog/archive/2008/12/14/squeezecenter-performance-on-qnap-ts109-ii
---

As promised in [Yesterdays
post](/blog/archive/2008/12/13/squeezecenter-on-qnap-ts-109), here are
some data on the performance of Squeezecenter on an QNAP TS-109 II
running [Debian Lenny](http://www.debian.org/releases/lenny/).

![Picture of QNAP TS-109 II](http://efod.se/media/blog/qnap_ts_109_ii.jpg)
My idea when buying the QNAP was to use it as a low-power alternative to
keeping my workstation switched on all the time for access to my music
collection from the Squeezebox.

Low power processors have a drawback, though - you don't get that much
processing power out of them. Running Squeezecenter on it turned out to
work.. but not very fast.

Memory Consumption
==================

The QNAP TS-109 II has 256Mb of memory. That's good, because
squeezecenter alone consumes about 70Mb of virtual memory, och which 60
is resident. The MySQL server started by squeezecenter will consume
another 97M virtual/20Mb resident. Part of the virtual memory used by
MySQL is probably mmap:ed files, and that doesn't really count.

With only squeezecenter and the standard set of daemons such as syslogd
and dhcpd running, and NFS server in the kernel, it seems like there's
not much swap usage, so the amount of available memory is not extremely
low. Don't try the 128Mb version of the QNAP, though, that will be
painstakingly slow because much more swap will be required.

Web Interface Performance
=========================

The web interface is rather slow. You have to wait several seconds
before things appear, and it also seems like the CPU consumption
increases significantly while using the web interface.

One strange thing is that the CPU consumption of the perl process is
very high, while the CPU consumption of the MySQL process is very low.
One has to wonder if the SQL database is used in an optimal way. Letting
the database do most of the work is often the best way to achieve good
performance. Doing a lot of processing after the data has been read from
the database is a bad way. But, I have not studied the database
operations in detail, this is just guesswork from my side.

Changing from the default skin to the *Classic* skin did help, but it's
still slow.

Using the Squeezebox to search for music
========================================

![Picture of idle Squeezecenter v3](http://efod.se/media/blog/squeezebox_idle.jpg)
Using the remote to search for music via the squeezebox has good
performance. Starting playback sometimes has a slight delay, which I
think in most cases is because of transcoding..

Transcoding Ogg Vorbis files
============================

The firmware for the Squeezebox has support for decoding Ogg Vorbis
files, but unfortunately it doesn't seem to work well at all. It can't
read about half of my Ogg Vorbis files. Even newly ripped files are
troublesome, and if I rip CD and code it into Ogg Vorbis, some of the
files will work in the Squeezebox, some will not.

Since I do have a lot of Ogg Vorbis files, the solution is to have
Squeezecenter transcode the Ogg data to another format that the
Squeezebox understands, before sending it over the network. This process
is called *transcoding*.

I first tried to transcode into
[FLAC](http://en.wikipedia.org/wiki/FLAC), but that was too
CPU-intensive for the QNAP TS-109 II to handle - probably because two
compressed formats were involved.

Transcoding from Ogg to [AIFF](http://en.wikipedia.org/wiki/Aiff) does
seem to work rather well - there is still a slight delay before you can
hear the music after pressing play on the remote.

An interesting experiment would be to use the integer-only Ogg decoder,
[Tremor](http://en.wikipedia.org/wiki/Tremor_(software)). That might
speed things up because as far as I understand, floating point
performance is not that good on the ARM architecture.

Conclusion
==========

Running Squeezecenter on the QNAP TS-109 II does work, but it's a bit
slow. Part of the problem is that Squeezecenter is rather bloated,
functionality-wise.

It's a pity the only documentation on the protocol used between
squeezecenter and squeezebox is the Perl source code.

