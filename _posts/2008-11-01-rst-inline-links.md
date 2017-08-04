---
layout: post
title: 'Inline links in reStructured Text'
tags: [software]
redirect_from: /blog/archive/2008/11/01/rst-inline-links
---

I've been using [reStructured
Text](http://docutils.sourceforge.net/rst.html) for documentation
purposes for a couple of years, but I have never read the full
specification, only the quick reference, and I probably read that
rather.. *quick*. So quick indeed that I have always been irritated
because I couldn't find how to write hyperlinks without having to list
them at the end of the document.

But today I found it. So here it is, for my future reference:

    Add a `hyperlink to reST <http://docutils.sourceforge.net/rst.html>`_

That's the quick-n-dirty variant. Here's the perhaps more readable, but
more cumbersome approach that I've been using until now:

    Add a `hyperlink to reST`_ 

    .. _hyperlink to reST: http://docutils.sourceforge.net/rst.html

