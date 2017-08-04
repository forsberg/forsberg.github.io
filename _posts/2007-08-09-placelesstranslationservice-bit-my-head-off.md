---
layout: post
title: 'PlacelessTranslationService bit my head off!'
tags: [open source,software,plone]
redirect_from: /blog/archive/2007/08/09/placelesstranslationservice-bit-my-head-off
---

Today, I made the mistake of adding a <myproductname\>-sv.po file in the
i18n directory of my product, which accidentally were marked with

    Language: en

This of course made the english strings appear in swedish, but that's
only to expect. What happened then was worse - after correcting the file
to contain:

    Language: sv

..there were no change! The english strings still appeared in swedish! \

After a frustrated debug session, it turns out that the language
property of the GettextMessageCatalog object stored in the ZODB (I
think) is not reloaded when the Language property in the file is
changed. So, even if you change the Language line in the .po file, the
translation will still be marked as being in the language it first was
entered as.

The solution? Move the .po-file out of the i18n directory, restart Zope,
then move it back, and restart again.

Gah! \

Well, at least I can be glad that my CMS is an open source product,
allowing me to debug problems properly.\

\


