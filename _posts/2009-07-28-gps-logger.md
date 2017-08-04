---
layout: post
title: 'Playing with a SkyTraq Venus GPS logger under Linux'
tags: [linux,gis]
redirect_from: /blog/archive/2009/07/28/gps-logger
---

I got a new toy today - a GPS logger. Got it as part of a magazine
subscription deal - two issues + GPS logger for about $12. That magazine
was not my kind of magazine, but getting a GPS logger delivered home for
$12 was worth having to throw away two magazine issues :-). For other
people trying to get this to work under Linux, the magazine in question
was [Aktiv Träning](http://www.aktivtraning.se).

After some fiddling, I came to the conclusion that the device is based
on the SkyTraq Venus chipset:

    skytraq: Venus device found: Kernel version = 1.3.3, ODM version = 1.4.5, revision (Y/M/D) = 07/12/11

After plugging the device into an USB port, it appears as a serial port,
in my case /dev/ttyUSB0. The data can be retrieved using
[GPSBabel](http://www.gpsbabel.org/), but it has to be the development
version - the stable version does not feature the [skytraq
driver](http://www.gpsbabel.org/htmldoc-development/fmt_skytraq.html)
required. The development version is available via CVS from sourceforge,
see
[http://sourceforge.net/projects/gpsbabel/develop](http://sourceforge.net/projects/gpsbabel/develop)
for details on how to access CVS.

Once you have the development version of gpsbabel, getting the data is
as easy as:

    ./gpsbabel -D 9 -i skytraq,initbaud=38400,baud=38400,erase -f /dev/ttyUSB0 -o gpx -F out.gpx

This will write the GPS coordinate log to *out.gpx* in the [GPS Exchange
format](http://www.topografix.com/gpx.asp) - a lightweight XML format.

The above command will also erase the log from the device, so the next
download contains just the latest log.

Since I like playing with [Google Earth](http://earth.google.com), I
also learned that the GPX can be converted into KML - the format Google
Earth can read, by running:

    ./gpsbabel -i gpx -f out.gpx -o kml -F out.kml

Just open *out.kml* with Google Earth, and you'll see where the GPS
logger has been.

On popular request, here's a few images of the device.

![Skytraq Venus device](http://efod.se/media/blog/skytraq_venus.png)
![Inside the battery compartment of a Skytraq Venus device](http://efod.se/media/blog/skytraq_venus_inside.png)
The label inside the battery compartment has the following text:

    GT-750F/L-Lite
    GPS Receiver(Data Logger)
    RoHS CE FCC ID:VHP-750F
    Made in Taiwan CANMORE

