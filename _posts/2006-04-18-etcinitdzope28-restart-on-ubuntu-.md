---
layout: post
title: '/etc/init.d/zope2.8 restart on Ubuntu '
tags: [plone]
redirect_from: /blog/archive/2006/04/18/etcinitdzope28-restart-on-ubuntu-
---

*/etc/init.d/zope2.8 restart* didn't work on my Ubuntu Server 5.10. It
turns out that it's using Ubuntu's homebrewn *dzhandle* script to handle
plone instances. You are supposed to create instances using dzhandle. If
you do, there'll be a file named *debian\_policy* in the *etc* directory
of the instance, and if that file exists, dzhandle will recognize the
instance and happily restart it.

