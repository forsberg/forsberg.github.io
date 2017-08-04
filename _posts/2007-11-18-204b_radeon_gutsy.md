---
layout: post
title: 'Samsung 204b + ATI Radeon 9250 SE - the saga continues'
tags: [hardware,linux,review,syncmaster_204b]
redirect_from: /blog/archive/2007/11/18/204b_radeon_gutsy
---

I've[previously
written](/blog/archive/2007/01/03/samsung-syncmaster-204b-r-dont-try-that-at-home "Samsung Syncmaster 204B [R] on DVI - don't try that at home!")
about my adventures in getting my Samsung 204b, made in Slovakia, to
work properly in 1600x1200 at 60Hz (short story: Can't be done due to
bugs in their DVI implementation). \

Yesterday, I decided to upgrade my home workstation from Ubuntu 7.04 to
7.10, and of course, the flickering screen syndrome came back.

After lot's of tests with many different options in
*/etc/X11/xorg.conf,* I got some help in a local forum, and came to the
conclusion that modifying xorg.conf doesn't help. Using the xrandr
command does however offer a way to solve the problem.

I how have the following list of commands in my */etc/kde3/kdm/Xsetup*
(I use kdm to start my X server, if you use another display manager,
adjust the path to one that makes sure the commands are run right after
X server startup):

    xrandr --newmode "1600x1200@55" 150.0 1600 1804 1996 2160 1200 1201 1204 1250 +hsync +vsyncxrandr --addmode DVI-0 1600x1200@55xrandr --output DVI-0 --mode 1600x1200@55

Gosh. Seems like there's some kind of bug in the ATI driver in the X.org
7.2 packaged with Ubuntu Gutsy, or perhaps in X.org itself.\


