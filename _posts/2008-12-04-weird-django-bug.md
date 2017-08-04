---
layout: post
title: 'Weird Django Bug'
tags: [software,django]
redirect_from: /blog/archive/2008/12/04/weird-django-bug
---

I think I hit [Django bug
\#6681](http://code.djangoproject.com/ticket/6681) yesterday. It's the
kind of bug that triggers only if three completely different conditions
are met at the same time, where at least one of them depends on timing.
In this case:

-   The Apache process must be recently started.
-   The first request hitting the Apache process must be for a page that
    requires reST rendering.
-   The reST must have a section that triggers the default interpreted
    role.

For reference, the exception was:

    AttributeError: Values instance has no attribute 'default_reference_context'

