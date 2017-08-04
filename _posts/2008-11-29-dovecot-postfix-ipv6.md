---
layout: post
title: 'Enabling IPv6 in Dovecot and Postfix'
tags: [linux,network,ipv6]
redirect_from: /blog/archive/2008/11/29/dovecot-postfix-ipv6
---

I realized after some testing that neither
[Postfix](http://www.postfix.org) (my MTA), nor
[Dovecot](http://www.dovecot.org) listened to IPv6 by default. In both
cases, enabling IPv6 was easy.

(This is where I found out that my algorithm for getting parts of an
entry and showing it on the front page doesn't work that well.. so
therefore, this text has been added, as it works as a workaround).

Postfix
=======

Set the *inet\_protocols* parameter in */etc/postfix/main.cf*:

    inet_protocols=all

The default value is *ipv4*.

Dovecot
=======

Set the *listen* parameter in */etc/dovecot/dovecot.conf*:

    listen=[::]

At least on Linux, this will make Dovecot listen to both IPv4 and IPv6.
Setting the value of listen to *\**, will make it listen only to IPv4.

Apache
======

My apache server happily picked up the presence of an IPv6 interface
after a restart. This is probably due to the fact that I have a the
following in my Apache configuration:

    listen=*

