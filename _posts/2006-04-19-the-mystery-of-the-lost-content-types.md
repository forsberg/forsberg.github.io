---
layout: post
title: 'The Mystery of the Lost Content Types'
tags: [plone]
redirect_from: /blog/archive/2006/04/19/the-mystery-of-the-lost-content-types
---

I was puzzled yesterday when I uploaded a file via WebDAV. Since the
file was equipped with a Content-Type header, I expected it to be parsed
as reStructured Text. Instead, it appeared as a DTML document. The
horror! The horror!

It turned out that the predicate list in the content\_type\_registry was
empty. I don't know why. I recently upgraded the Plone instance from
2.1.0 to 2.1.2, that could be related.

By removing and then reinstalling the ATContentTypes product with the
Add/Remove Products tool, the problem went away.

Odd.

