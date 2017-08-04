---
layout: post
title: 'Easy Update of Slicehost DNS Entries'
tags: [misctools,python]
redirect_from: /blog/archive/2010/02/06/slicehost-dns-api
---

This website runs on a virtual machine I buy from
[Slicehost](http://www.slicehost.com/). I've also choosen to use their
DNS servers for my domain - the service is stable and included in the
price.

The Slicehost DNS can be modified using the [Slicehost
API](http://articles.slicehost.com/2008/5/13/slicemanager-api-documentation).
I wrote two small scripts for easy modification of Slicehost DNS entries
from the commandline or from scripts.

-   `update_entry`, for adding or updating existing entries.
-   `dhclient_update_hook`, which very easily can be used to update an
    entry from a dhclient script, to keep records that point to dynamic
    adressess updated automatically.

Both are available from by cloning my [misctools
project](http://github.com/forsberg/misctools/tree/master/slicehost/) at
[GitHub](http://github.com).

