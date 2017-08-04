---
layout: post
title: 'Sometimes, there''s a Product Just For You'
tags: [plone]
redirect_from: /blog/archive/2006/02/23/sometimes-theres-a-product-just-for-you
---

Today, the marketing person at work came and told me that he wanted a
signup form for a usergroup meeting we're planning. Something simple
that mailed him with the relevant information.

-   *"OK, I'll go see if I can fix something like that.."*

I had heard about
[PloneFormMailer](http://plone.org/products/ploneformmailer) earlier, so
I did some quick research on it, including asking on \#plone to verify
that it works in Plone 2.1, and installed it in my staging instance.

It solved my problem perfectly!

This is one of the things I like about plone - very often, someone else
has already solved the web publishing problem you're having right now,
and you can use an existing product instead of having to create your
own.

[PloneFormMailer](http://plone.org/products/ploneformmailer) uses
[Formulator](http://www.zope.org/Members/infrae/Formulator), which also
looks very interesting for some of my needs - for example, I have a
custom-written product that fiddles with some LDAP values, and I could
probably use Formulator or some other similar product. [this
HOWTO](http://plone.org/documentation/how-to/integrating-form-controller-with-formulator)
seems interesting.

