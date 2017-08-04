---
layout: post
title: 'Deleting Amazon S3 buckets using Python'
tags: [software,misctools]
redirect_from: /blog/archive/2009/08/09/delete-s3-bucket
---

For a while, I used
[Duplicity](http://rdiff-backup.stanford.edu/duplicity.html) to make
backups to an Amazon S3 bucket. That kind of worked, but I had to do a
lot of scripting myself to get it working automatically, so after
finding out about [Jungledisk](http://www.jungledisk.com/), I switched
to that. Jungledisk has a nice little desktop applet that keeps track of
doing my backups while my computer is on, etc. That's convenient.

Anyway, the Duplicity/S3 experiments left me with an Amazon S3 bucket
with about 9000 objects. Getting rid of that proved to be something of a
challenge - you have to delete all objects inside the bucket before you
can delete the bucket itself, and there's no API call for doing that. I
also tried the web application for managing buckets,
[S3FM](http://s3.amazonaws.com/s3fm/index.html) but that didn't cope too
well with that many objects - my web browser just hung.

I have to admit I could have put more effort into googling before
solving it by writing my own script - but writing my own script was more
fun :-).

My script managed to delete all 9000 objects without trouble, although
it did take quite a while to complete - I let it run overnight.

If you need to do the same thing, it's available here:

[](http://github.com/forsberg/misctools/tree/0d6cbd189b80e52501d94742fa04bba36b7f34a6/S3)

[StackOverflow](http://stackoverflow.com) has several other solutions:
[](http://stackoverflow.com/questions/27267/delete-amazon-s3-buckets)

