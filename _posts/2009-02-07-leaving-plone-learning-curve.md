---
layout: post
title: 'Why I left Plone - Part 1, the Learning Curve'
tags: [plone,noplone]
redirect_from: /blog/archive/2009/02/07/leaving-plone-learning-curve
---

For a long time, I was a [Plone](http://plone.org/) user and developer.
I tried hard to keep myself convinced that Plone was the solution to
many web-related problems, not only strictly Content Management-related
ones, but all sorts of web applications.

A while ago, I realized that I was, just that - *trying hard to keep
myself convinced*. That is really not a good sign when it comes to
frameworks you use in your programming - if you're to work with them and
get productive, you have to like them because they *actually* are good,
and *fun*, to work with. This is not the case with Plone, and I'll try
to explain why.

After starting to write this, I realized that I have so many reasons to
leave Plone that this will have to be the first in a series of posts.
Stay tuned!

The Learning Curve
==================

I started using Plone while looking for a good solution for the external
website of the company I was then working for. After some evaluation of
different alternatives, I decided on Plone. Plone was then at version
2.0.6, if I recall correctly.

We hired a summer intern with some previous Plone experience with the
task of doing different kinds of integration with our existing systems,
including some LDAP integration. I remember that he was spending lots of
time cursing especially the LDAP integration and the user management
code.

About the time when the integration were finished and we began thinking
about deplying, Plone 2.1 was released.

![Explosion](http://efod.se/media/blog/explosion1.png)
**KABOOM** - an explosion of new things to learn!

Plone 2.1 was like an entirely new piece of software. Lot's and lot's
and *lot's* of things had changed. At least that was the impression you
got if you were not a *Plone Guru*.

I made the decision of going for Plone 2.1, since I didn't want us to be
left behind with incompatible Products (that's the Plone term for more
or less useful addons that can be downloaded and installed in a Plone
instance - I'll probably write something about them later..). So, lot's
of time had to be spent *again* trying to fixup the site into a usable
state. The LDAP integration we hoped for had to be half-ditched because
of time constraints, and we also had to lower the ambitions on the
creation of a nice-looking graphic appearance, instead reusing some old
CSS we alread had. Even then, fighting the Plone styles system was a
pain, and it didn't really get better in later versions.

We finally got the site deployed. It didn't get updated as often as I
had hoped for, and frankly, it didn't work that well, with hickups and
performance trouble.

After a few years, Plone 2.5 arrived.

![Explosion](http://efod.se/media/blog/explosion2.png)
**KABOOM** - an explosion of new things to learn!

This was where the magical mystery tour of Zope3 technology began to
show its ugly face in the code. You had to learn stuff like adapters,
interfaces, etc. And although these are well known concepts in the
programming world, the key is to neither *overuse* them nor
*overcomplicate!*

I don't remember, but I *think* I managed to lift the site up to Plone
2.5. I was really starting to get tired of Plone at this point.

The fun however didn't end there, because some time later, Plone 3
arrived. And again.. **KABOOM** - lot's of new things to learn. To be
just, some of the new things were already familiar if you had learnt
them in Plone 2.5, but there were still plenty of new weirdness.

![Explosion](http://efod.se/media/blog/explosion3.png)
For me, not being a full time web site developer, it was near to
impossible to keep track of all changes and concepts. It was especially
hard to know which concepts to use for good compatibility with future
versions of Plone.

New things arrived all the time - one example being the way you were
supposed to make skins (the graphic appearance). It was completely
revamped several times, each time introducing new layers of abstraction
and complexity. Stuff like the stylesheet registry, where you are
supposed to write XML code that registers your stylesheets in a magic
registry that's accessible only via the magic web interface (the ZMI).
Argl!

Trying to manage the way installations are made became more and more
complicated, being a python script to begin with, then growing into
countless XML files per product, making it very hard to keep track of
what's going into what file. Argl, again!

No, I'm all happy I left Plone, and the learning curve is just one of
the reasons.

(Beautiful explosion images from [PD
Photo.org](http://pdphoto.org/PictureDetail.php?mat=pdef&pg=8344))

