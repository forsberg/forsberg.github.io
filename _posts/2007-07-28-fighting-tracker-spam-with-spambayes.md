---
layout: post
title: 'Fighting tracker spam with SpamBayes'
tags: [open source,software]
redirect_from: /blog/archive/2007/07/28/fighting-tracker-spam-with-spambayes
---

During the last few days I've had time to do some programming just for
fun. When you combine vacation and bad weather, you can be very
productive :-).

Most of the time, I've been doing work for the roundup tracker instance
for the python development team. I [wrote about the new
importer](archive/2007/07/25/life-as-a-sf-net-conversion-script-author "Life as a sf.net conversion script author")
earlier, and now I've also created an anti-spam system based on
[SpamBayes](http://spambayes.sf.net). \

For those interested, there's a [technical description of the roundup
spambayes
integration](http://www.mechanicalcat.net/tech/roundup/wiki/SpamBayesIntegration)
in the roundup wiki.

SpamBayes seems to be a nice piece of software, especially now when it
has an XMLRPC interface. Imagine having a SpamBayes XMLRPC server on
your network, and then a plugin in your mail user agents that calls it
to rate messages before sorting them down to folders, and a button in
the user interface that allows users to report messages as being spam or
legitimate content. That would be very powerful and give very few
incorrect ratings as each organisation's SpamBayes server would learn
what's legitimate content for the organization where it's installed. \

### When to sort?

As all users receiving large amounts of mail (in my case mostly because
of mailing list subscriptions), I sort my mail. For my personal mail, I
let the [Cyrus IMAP](http://cyrusimap.web.cmu.edu/) server sort whenever
the messages arrive, using the Sieve sorting language. I use the Sieve
filter interface in [Squirrelmail](http://www.squirrelmail.org/) to
create rules. This is very convenient as the mail is always sorted when
I arrive at my mail client, regardless of which client I use. Also, I
only have to define my filter rules at one place. I only wish there were
more mail user agents with decent Sieve filter support.\

For sorting out spam however, the later the sort is done, the better, at
least for some kinds of anti-spam measures, including statistical
filters such as SpamBayes. Imagine the following scenario:\

-   User A, who likes to arrive at the office early in the morning,
    opens his INBOX and find 2 messages that have been incorrectly
    classified as legitimate mail. He presses the 'report as spam
    button', which in an ideal world will teach the local SpamBayes
    server to score the message better.
-   User B, who is a lazy bastard, arrives two hours later. When his
    mail user agent sorts his mail using the local SpamBayes server, he
    can benefit from the work made by User A earlier in the morning, as
    the two messages are now correctly sorted. \

On the other hand, the statistical filters seems to work well enough for
the typical spam that sorting early (on the server) is probably good
enough, so I think I'll continue to let my Cyrus IMAP do the sorting for
me. A button in my mail user agent for classifying the message would
still be neat, though. \


