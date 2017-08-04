---
layout: post
title: 'Simple Parallelization with xargs'
tags: [parallelization]
redirect_from: /blog/archive/2009/05/30/parallelization-with-xargs
---

If you run a modern computer, chances are high that you have a
multi-core processor. That forces us into paralell programming to get
more performance, which is much harder than doing serial programming.

The operating system and existing shell commands can do much for us,
though. Let's say you have a bunch of files where each should be
processed by a command. Of course, with multiple cores, this could be
sped up by running multiple instances of the command simultaneously. And
there's a very easy way to do that - *xargs*. An example for converting
raw files into jpeg:

    find . -type f -name '\*.CR2' \|xargs -n 1 -P 3 ~/bin/raw2jpeg

This will find all files named *\*.CR2* and feed that list to *xargs*,
which will run up to three (-P 3) processes simultaneously, giving each
command one filename (-n 1) on its commandline.

