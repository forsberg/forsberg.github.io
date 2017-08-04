---
layout: post
title: 'efod.se - now with nice looking titles on WebDAV-uploaded HTML!'
tags: [plone]
redirect_from: /blog/archive/2006/02/28/efodse---now-with-nice-looking-titles-on-webdav-uploaded-html
---

Plone 2.1-2.1.2 has an irritating bug - HTML files uploaded via WebDAV
gets the filename as page title, which looks very ugly.

I've now created a patch for this that restores the behaviour of Plone
2.0.x, where the title is extracted from the <title\> tag.

Check out
[https://dev.plone.org/plone/ticket/4877](https://dev.plone.org/plone/ticket/4877)
for the patches. I'm now eagerly awaiting feedback from the Plone
developer responsible for the bug.

