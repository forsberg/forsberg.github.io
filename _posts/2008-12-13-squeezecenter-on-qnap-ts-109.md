---
layout: post
title: 'Running Squeezecenter on QNAP TS-109 II'
tags: [hardware,turbostation,squeezebox]
redirect_from: /blog/archive/2008/12/13/squeezecenter-on-qnap-ts-109
---

I have now managed to get
[Squeezecenter](http://www.slimdevices.com/su_downloads.html) running on
my QNAP TS-109 II. Squeezecenter is the server a
[Squeezebox](http://www.slimdevices.com/pi_squeezebox.html) network
music player connects to in order to get hold of its music.

![Picture of QNAP TS-109 II](http://efod.se/media/blog/qnap_ts_109_ii.jpg)
Since the QNAP TS-109 II is running on the ARMEL architecture,
installation was a little bit tricky.

Squeezecenter is written in [Perl](http://en.wikipedia.org/wiki/Perl).
Let me state early that [Perl](http://en.wikipedia.org/wiki/Perl) is
**not** my favourite programming language.

I installed the Debian package of Squeezecenter 7.3 available
[Slimdevices web](http://www.slimdevices.com/su_downloads.html). The
package's architecture is *all*, which is not true - it contains [Perl
XS](http://en.wikipedia.org/wiki/XS_(Perl)) code compiled for i386 and
amd64. This code won't run on ARMEL.

The Squeezecenter package also ships lot's and lot's of third party Perl
modules, but they don't work on Perl 5.10 because of module version
conflicts. I run [Debian Lenny](http://www.debian.org/releases/lenny/)
on the QNAP, and guess which Perl version is shipped with Lenny... Yep,
Perl 5.10.

I found [an excellent forum
post](http://forums.slimdevices.com/showpost.php?p=300276&postcount=22)
by "bugfixer" at the squeezebox forums explaining how to get
Squeezecenter running on Perl 5.10. Much of the information in this
blogpost comes from that post.

The shipped perl modules are all available as Debian packages - with one
exception - the libjson-xs-perl package in Debian lacks the file
*/usr/lib/perl5/JSON/XS/VersionOneAndTwo.pm*, so I had to copy that one
from the version shipped with squeezecenter.

The squeezecenter Debian package also has a large amount of dependencis
not listed in the package's metadata. And to add to the misery, it
requires the perl package *Encode::Detect*, which is not even available
as Debian package.

To avoid having to keep track of this mess, I created a
[puppet](http://puppet.reductivelabs.com/) class which installs all
dependencies, installs squeezecenter, and then removes all files which
cause trouble. With that work done, I can reinstall squeezecenter and be
pretty sure it will work. I did an upgrade of squeezenter today by
downloading the new squeezecenter debian package, installing it, then
ran puppet to move away all the offending perl classes - worked as a
charm!

So, if you want a list of all packages required and all files that must
be moved, refer to [the source for my squeezecenter puppet
class](http://efod.se/media/squeezecenter.pp). That list will be kept
more up to that than if I would list the info on this blog post.

I'll be back with some info on the performance when running
Squeezecenter on the QNAP. I can say already that it's **not** blazingly
fast..

