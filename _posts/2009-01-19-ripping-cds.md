---
layout: post
title: 'Ripping 300 CDs..'
tags: [linux,squeezebox]
redirect_from: /blog/archive/2009/01/19/ripping-cds
---

I'm currently in the process of transferring my CD collection into
digital format for use with my
[Squeezebox](http://efod.se/blog/tags/squeezebox/). This is a major
project when you own around 300 CDs..

![Stack of CDs](http://efod.se/media/blog/rip_cds.jpg)
Ripping CDs, but to what format?
================================

I did some thinking and evaluation before choosing format for the
storage of my CDs in digital format;

Ogg Vorbis
----------

[Ogg Vorbis](http://www.vorbis.com/) was one of the alternatives. It is
*patent free*, which would fit my free software background. There are a
whole bunch of devices supporting it, but with the
[SO](http://en.wikipedia.org/wiki/Significant_other) buying a new mp3
player that didn't support Ogg, and the
[Squeezebox](http://efod.se/blog/tags/squeezebox/) only half-supporting
it, Ogg was unfortunately not an alternative.

FLAC
----

[FLAC](http://flac.sourceforge.net/) were another alternative. Free, and
also lossless - the thought of actually *storing* the CDs without loss
of data was tempting. Again, it fell on compatibility. Finding devices
such as mp3 players and car audio equipment.

One option would have been to store as FLAC and then recode everything
to mp3, possibly on demand, but I demeed that out as too much work with
little gain.

MP3
---

So, as you might have guessed, for compatibility, I choose to rip my CDs
to mp3. I'm using the [LAME](http://lame.sourceforge.net/) encoder with
the best quality variable bitrate (VBR) encoding. According to the
[Hydrogen Audio
Wiki](http://wiki.hydrogenaudio.org/index.php?title=Lame), LAME has the
best VBR encoder out there.

The resulting MP3's play directly on the
[Squeezebox](http://efod.se/blog/tags/squeezebox/) hardware without
problems, and works as intended in the SO's mp3 player as well.

