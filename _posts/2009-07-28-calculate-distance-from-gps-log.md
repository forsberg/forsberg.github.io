---
layout: post
title: 'Calculating the Distance of a GPS log'
tags: [linux,gis]
redirect_from: /blog/archive/2009/07/28/calculate-distance-from-gps-log
---

Playing with my GPS logger, I wanted to know the distance travelled
between all the points in a GPS log. For example, if I went for a
bicycle trip and brought the logger, it would be nice to know how many
kilometers I have travelled.

Trying to find a tool that did this without being cumbersome to use
proved more difficult than I thought, so I did a quick hack with the
help of the python bindings for [gpsd](http://gpsd.berlios.de/). It's a
very simple script:

    $ ./distance.py promenad2.gpx 
    427.077378454

Given a [GPX file](http://www.topografix.com/gpx.asp), it will print out
the number of meters travelled.

Fetch it [in the fgpstools
repository](http://github.com/forsberg/fgpstools/tree/master) on
[github](http://github.com)

