---
layout: post
title: 'Slow Puppetmaster? Check your reverse DNS'
tags: [puppet]
redirect_from: /blog/archive/2011/01/13/puppetmasterd_reverse_dns
---

Yesterday some of the servers I care for at work were moved to a
different network. After the move, all puppetd runs started to take a
very long time. Where it would usually take 10-15 seconds, it now timed
out with errors like:

    Jan 12 19:39:16 host1 puppetd[15760]: Calling puppetmaster.getconfig
    Jan 12 19:41:16 host1 puppetd[15760]: Configuration retrieval timed out

(Note the two minutes between the informational message about calling
puppetmaster.getconfig, and the timeout)

Highly confusing, especially since puppetd was slow not only on hosts
which had moved to the new network, but also on hosts which had not
moved.

The reason turned out to be slow reverse DNS for the new network range.
Puppetmaster it seems is doing lot's and lot's of DNS lookups for
clients, and that seems to be a synchronous operation. I think what
caused all hosts to slow down was that puppetmaster got busy looking up
one of the hosts on the new network, and that would cause the request
from a host that had not moved to be put on hold.

Fixing the DNS issue solved the problem.

This is on puppet 0.24.5. Later versions might have a better behaviour.

