---
layout: post
title: 'RSH - an unpleasant guest from the past'
tags: [software,sugarcrm]
redirect_from: /blog/archive/2006/03/04/rsh---an-unpleasant-guest-from-the-past
---

Yesterday I spent some time evaluating the Open Source version of
[SugarCRM](http://sugarforge.org), since the salespeople at work wants
to see if a CRM can help them.

I installed an extension called
[ZuckerMail](http://www.sugarforge.org/projects/zuckermail/) to allow
reading of mail stored on our IMAP server, and was irritated by the long
time it took to get the list of mail, or to read a single mail.

I did some strace:ing, but that didn't help very much - it only revealed
the fact that something was waiting for 10 seconds. A process listing
however revealed that there was several rsh procesess trying to contact
the IMAP server. Also, my firewall's log had blocked several connection
attempts from this machine to the IMAP server on port 22 (ssh).

Aha.. but why!

It turns out that the IMAP library for PHP is built on top of the
ancient c-client library from the UW IMAP. If you're trying to make an
connection without explicitly telling it that you want to connect with
ssl (something the GUI for configuring the connection did not have an
option for - only STARTTLS, which is another thing), the c-client
library tries to run rimapd on the host via rsh. There is a /usr/bin/rsh
on the machine, linked to /usr/bin/ssh via /etc/alternatives (Debian
sarge).

You can turn this behaviour off in a configuration file for c-client. I
solved the problem a bit more drastically - by removing /usr/bin/rsh.
This made all IMAP operations go much faster.

