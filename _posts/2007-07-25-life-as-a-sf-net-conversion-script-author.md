---
layout: post
title: 'Life as a sf.net conversion script author'
tags: [open source,software]
redirect_from: /blog/archive/2007/07/25/life-as-a-sf-net-conversion-script-author
---

About a year ago, the infrastructure team of the [python language
project](http://python.org)sent out a [call for
trackers](http://wiki.python.org/moin/OriginalCallForTrackers). They had
come to the conclusion that the tracker available at sourceforge was not
good enough. I can understand that - it's very hard to use, and since
it's running on sourceforge's servers, it can't be customized.

\

I and several other people thought that
[roundup,](http://roundup.sf.net) a tracker infrastructure would be a
good choice, so we formed a team and managed to come up with a
submission for the call. This included writing a conversion script that
took the data from sourceforge and imported it into the new tracker. I
created this script based on a screenscraper library for sourceforge
written by Fredrik Lundh. This was importer \#1.\

Later on, roundup was selected as one of the two final alternatives.
Happy happy, joy joy :-). A team was formed (including me) for creating
the tracker, and [Upfront Systems](http://www.upfrontsystems.co.za)
kindly provided a linux host for running the tracker. \

Now began the real work of designing the tracker and adjusting the
importer to the final schema. During this time, sourceforge managed to
fix their broken xml export, so I wrote a new importer that instead of
screenscraping webpages took an xml file as input which was much faster
and more reliable. That is, I wrote importer \#2.

Later on, when we were beginning to get ready for production launch, a
real showstopper shows up - the xml export from sourceforge couldn't
cope with the size of the python project - the export was missing data.

After several months of waiting for sourceforge, they have a new export
script that includes all data. Unfortunately, it has a completely new
xml format. Writing a third importer was less than fun, but I managed to
complete importer \#3 yesterday. Hopefully, I didn't introduce that many
bugs.. \

Who knows, maybe the python project will have a new tracker sometime
this year? :-)

Try out the new tracker at
[http://bugs.python.org](http://bugs.python.org).\


