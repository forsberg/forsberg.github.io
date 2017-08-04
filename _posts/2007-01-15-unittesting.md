---
layout: post
title: 'Yes, unit testing can be fun :-)'
tags: [software,testing,software engineering]
redirect_from: /blog/archive/2007/01/15/unittesting
---

Yesterday, I read one of the [teaser
chapters](http://www.pragmaticprogrammer.com/starter_kit/utj/whatis.pdf)
of [Pragmatic Unit Testing in Java with
JUnit](http://www.pragmaticprogrammer.com/starter_kit/utj/index.html).
It was a very interesting chapter, so I eventually ordered the book. \

According to the reviews and from the looks of the table of contents, it
doesn't talk too much about JUnit, but instead about general unit
testing methodology in general which is what I want, as I don't do Java
programming unless I can avoid it (another book on my bookshelf is btw
[Beyond Java](http://www.oreilly.com/catalog/beyondjava/), and although
I think the author believes a bit much in XML as a must for the future,
I feel that most of the conclusions in that book are something I can
agree with - Java is on its way out, except as a niche language for
"enterprise" applications. I don't know what *"enterprise"* is supposed
to mean - *"expensive and slow",* perhaps?

Anyway, today at work, I had to rewrite a function that reads
*/etc/ldap.conf* and parses out some LDAP server connection info. I had
to read in more data, and change its API slightly as it was limited in
the amount of data it could return. Inspired by the book, I started by
writing some unit tests (using [PyUnit](http://pyunit.sf.net)) and then
added more as I added features to the function.

Being able to run the tests while adding features, making sure that
adjustments to parse and return a new type of data didn't break old
data, made me fee happy and productive. Having to think about what kind
of data should be returned and therefore tested also gave a better and
more complete design.

In short - I'll be writing more unit tests from now on. I'm sure the
book (when it arrives) will give me plenty of inspiration. \

\

[\
](http://www.pragmaticprogrammer.com/starter_kit/utj/index.html)

