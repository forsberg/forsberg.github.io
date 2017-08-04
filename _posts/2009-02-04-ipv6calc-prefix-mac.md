---
layout: post
title: 'Calculating the automatically assigned IPv6 adress given prefix and MAC'
tags: [network,ipv6]
redirect_from: /blog/archive/2009/02/04/ipv6calc-prefix-mac
---

Today I had the need to calculate the automatically assigned IPv6 adress
I knew a host probably had since the network has a router advertisment
daemon.

I knew the network prefix and the hardware address (MAC/EUI-48). I
suspected [ipv6calc](http://www.deepspace6.net/projects/ipv6calc.html)
could probably do the job, but I had great trouble finding out how. I'm
sure the commandline syntax for ipv6calc makes sense once you get used
to it..

Anyway, here's how, for my own and your future reference:

::

> ipv6calc --in prefix+mac --action prefixmac2ipv6
> 2001:aaaa:bb:cccc::/64 AA:BB:CC:DD:EE:FF --out ipv6addr

IPv6 prefix as well as MAC obfuscated to protect the innocent.

Relevant links:

-   [[http://www.faqs.org/rfcs/rfc2373.html](http://www.faqs.org/rfcs/rfc2373.html)](http://www.faqs.org/rfcs/rfc2373.html)
-   [[http://packetlife.net/blog/2008/aug/04/eui-64-ipv6](http://packetlife.net/blog/2008/aug/04/eui-64-ipv6)/](http://packetlife.net/blog/2008/aug/04/eui-64-ipv6/)


