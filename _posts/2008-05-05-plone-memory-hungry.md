---
layout: post
title: 'Plone and 256Mb - forget that'
tags: [plone]
redirect_from: /blog/archive/2008/05/05/plone-memory-hungry
---

Quoting myself from the other day:

> ''It actually seems like Plone 2.5 can run on a machine with only
> 256Mb of memory with acceptable performance as long as the CPU is
> fast.''

Very wrong for my instance. At least if there is anything else running
on the machine, in this case a mail server (Postfix+Dovecot). Sloooow..

Resized my slice from 256M to 512M. Seems to work better now.

