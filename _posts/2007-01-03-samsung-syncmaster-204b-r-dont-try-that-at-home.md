---
layout: post
title: 'Samsung Syncmaster 204B [R] on DVI - don''t try that at home!'
tags: [hardware,linux,syncmaster_204b]
redirect_from: /blog/archive/2007/01/03/samsung-syncmaster-204b-r-dont-try-that-at-home
---

**Note:** *This instruction is valid for the ATI driver included with
Ubuntu Feisty Fawn (7.04). There's [another
entry](../../11/18/204b_radeon_gutsy "Samsung 204b + ATI Radeon 9250 SE - the saga continues")on
how to get it working in Ubuntu Gutsy (7.10).*\

I recently decided that it was time to replace my old trustworthy Nokia
Multigraph 446XPro CRT display with a flatscreen. The 446XPro has server
me well at various computers at home since 1998 (that's *eight years!*)
but it was time for something less space-consuming on my desk. Also, I
like the feeling of not sitting in front of an electron beam several
hours a day.

My list of specifications for the replacement was rather short:\
\

-   Must handle a resolution of 1600x1200 (I've been working with this
    resolution for many hours a day for the past 8 years, so I'm quite
    used to it)\

-   Adjustable height
-   Reasonable price

After some research, I bought a [Samsung Syncmaster
204B](http://www.samsung.com/Products/Monitor/LCD_Digital/LS20BRDBSQXAA.asp)
which seemed to be a reasonable fit given my specifications. As we'll
see, the word *Syncmaster* is somewhat ironic in the name of the
product... Also, it turned out that I got a Samsung Syncmaster 204B
**[R]**, which turned out to be very significant..\
\
I got the screen just a few days after ordering it, and connected it to
my graphics card, a ATI Radeon 9200SE, via analog VGA. After adjusting
the vertical refresh to the recommended 60Hz, I got the display working,
but with some distortions which made it hard to work with given the high
resolution and the small font I use for displaying information. This was
a disappointment. Obviously, the VGA decoder in the screen is not good
enough to handle the recommended solution.\
\
As a colleague of mine had similar trouble at work and solved them by
switching to a graphics card with DVI output, I decided to go the easy
way and buy a new graphics card, as the graphics card I had lacked DVI
output. It turned out that the 9200SE was the very *last card* in the
series that only had analog VGA output. My usual luck with hardware..\
\
I bought a ATI Radeon 9250 as replacement and installed it. This gave me
a sharp image. Yay! Or so I thought, because now, the screen started to
go blank now and then with irregular intervals. It went completely black
and then came back after half a second or so. Boy, that's irritating!\
\
After many attempts, I managed to find the right words that made Google
lead me right. [This forum
article](http://forums.entechtaiwan.net/viewtopic.php?=&p=17727) led me
to[this forum
article](http://www.evga.com/community/messageboard/post.asp?method=TopicQuote&TOPIC_ID=19835&FORUM_ID=32)
which describes the problem - it's a bug in the DVI implementation of
Syncmaster 204B [R]. It can't handle the bandwidth. Gah! My usual luck
with hardware..\
\
The forum articles says this bug appears only on Syncmaster 204B
**[R],** and only on models made in China. The latter seems not to be
true, as mine is made in Slovakia.\
\
There's a workaround - by lowering the vertical refresh to 56Hz, the
problem goes away.\
\
I'll do what I can to get a new screen without this bug anyway.\
\
[Here's my xorg.conf I use with the Radeon 9250 and the
Syncmaster.](/images/django2jekyll/migrated/blog-archive-2007-01-software-configuration-syncmaster-9250-xorg.conf "xorg.conf for a Samsung Syncmaster 204B [R] on ATI Radeon 9250")\


