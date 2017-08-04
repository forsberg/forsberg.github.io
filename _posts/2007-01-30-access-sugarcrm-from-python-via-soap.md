---
layout: post
title: 'Access SugarCRM from Python via SOAP'
tags: [software,sugarcrm,soap]
redirect_from: /blog/archive/2007/01/30/access-sugarcrm-from-python-via-soap
---

I spent part of the evening writing the embryo of a python module that
will hopefully make it easy to access [SugarCRM](http://sugarcrm.com)
from Python via SOAP. \

Right now, it only contains code for adding, updating, getting and
deleting Accounts, but that could easily be extended. A bunch of unit
tests too. \
Not very useful unless you're a developer. You need the [Zolera Soap
Infrastructure](http://pywebsvcs.sourceforge.net/) to get it to work.

Get the code from SVN:\

    svn co http://lsvn.lysator.liu.se/svnroot/forsberg/sugar_python/trunk 

\
See also:\

-   [ZSI vs. SugarCRM,
    1-0](archive/2006/09/13/zsi-vs-sugarcrm-1-0 "ZSI vs. SugarCRM, 1-0")\


