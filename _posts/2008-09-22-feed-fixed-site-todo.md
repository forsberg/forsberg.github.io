---
layout: post
title: 'Feed Fixed. Site Todo.'
tags: [django]
redirect_from: /blog/archive/2008/09/22/feed-fixed-site-todo
---

Yesterday evening was one of those frantic hacker moments when you
*really really* want to get the piece of software you've been working on
for a while up and running, even if it's getting really late and you
know you have to get up early the next morning. The broken feed, showing
pseudo-HTML to the user, was one effect of that. Has now been fixed by
use of the [safe filter
tag](http://docs.djangoproject.com/en/dev/ref/templates/builtins/#tfilter-safe).

One interesting thing is that [Google
Reader](http://www.google.com/reader) thought all my entries were new,
even though I made sure the timestamps in the RSS were identical. Might
have had to do with the change of the GUID-values in the feed, from a
*$£@¡$£!!* plone probably archetypes-hexadecimal thingie into the KISS
solution - the URL to the entry. [Planet
Lysator](http://planet.lysator.liu.se) seems to have behaved correctly,
displaying only the new entry.

Lot's of stuff still on the todo for this site, for example:

-   Better Navigation.

-   Catchier frontpage.

-   Photo album integrated with rest of site, to make it easy to link to
    photos from other kinds of content. A Photo feed, perhaps?

-   Make code for site available to the world.

-   A blog entry on how I converted from Plone to Django. Make
    conversion code available to the world -
    [Done](/blog/archive/2008/11/01/migrate-plone-to-django).

-   Some kind of more or less automatic moderation of comments, I've
    already received some spammy ones.

-   Preview in edit-mode when writing blog and CMS/content entries in
    [reST](http://docutils.sourceforge.net/rst.html).

-   A blog entry on why I've switched from Plone to Django..

All of this have to wait for another day, because now is time to sleep.

