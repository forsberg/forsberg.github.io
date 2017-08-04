---
layout: post
title: 'Network Solutions and their routines for outbound domain transfers'
tags: [general]
redirect_from: /blog/archive/2006/01/07/network-solutions-and-their-routines-for-outbound-domain-transfers
---

At work, I had a .com domain registered with [Network Solutions
Inc.](http://www.networksolutions.com) (from now on referred to as NSI).
This was not by purpose, but for historical reasons - it was registered
at a time when the only .com registrar was networksolutions.

It was getting near the time of renewal, so yesterday I decided I should
try to move it to [GANDI](http://www.gandi.net), where we have the rest
of our .com-domains registered. We like [GANDI](http://www.gandi.net),
they are easy to deal with and their web interface is designed to be as
helpful as possible, not to make it hard to do things, something which
seems to be the main design criteria for the web site of NSI.

That GANDI, who are based in France, sometimes forgets to translate one
or two words from french to english, and that the word order of some of
the sentences are french rather than english is just.. charming! :-)

The process of changing domain registrar turned out to be really
time-consuming, mostly because of NSI doing all they can to keep their
customers by confusing them. In a perfect world, companies would compete
by providing advantages to the customer, not by making it extremely
difficult to switch to another, competing, company.

To transfer a domain from NSI to GANDI, you have to:

1.  Unlock the domain from unathourized transfer at NSI.

    Now, to do that, you must login as a user which is the primary
    contact. In my case, that was not the user I had access to, but
    fortunately, I had access to the e-mail account registered with that
    user, so I could fetch a new password and login.

    This is the first overcomplicated part of the NSI administrative
    website - it has too many roles, with too many configurable
    permissions. It probably fits big hierarchial american companies,
    but for small users, it just sucks. Keep It Simple, Stupid (*KISS!*)

2.  Wait for NSI to update their whois records. In my case, this took
    about 24 hours. Well done, NSI. I guess they stick a piece of paper
    with the domain name change to go into whois to a
    [turtle](http://www.turtles.org/dedicate/dedicate.htm) who has to
    crawl a hundred meters over a highway before reaching the next
    administrative station where they actually change the data in whois.

    My turtle must have been killed in the first run, because I had to
    try twice.

    Poor turtle.

3.  Initiate the transfer at Gandi. You can't do that until the WHOIS
    information is updated, because it says the domain is locked from
    domain transfer.

4.  Find out that the whois data is still flawed - the primary
    administrative contact, which the NSI website indicated I was logged
    in as, had a correct mail adress listed. In whois, another,
    incorrect mail adress was listed. It turned out that there were two
    accounts with the name 'AAA BBBBBBB', and the second one, the one
    with the incorrect mail address, was listed in whois.

    After a while, I found a part of the NSI website which was
    completely new to me, where you could actually change which
    information was set in whois. Again, overcomplicated - one
    administrative contact should be enough, always being the same in
    both the web interface and in whois.

    This time, they sent another turtle (a cousin of the first turtle)
    with a small rocket motor attached, which flew over the highway to
    the whois department, because this change, got into whois almost at
    once. Unfortunately, the poor turtle smashed into the wall of the
    whois department and was killed.

    Poor turtle. Not only was he mourning his cousin. Now he was himself
    killed in the dangerous whois update business.

5.  Re-initiate transfer.

6.  Receive mail from Gandi to confirm that domain should be moved.
    Reply to this with accept code. Get confirmation from Gandi that
    reply mail was received.

    At this stage, you have been assigned a dynamic web page at Gandi
    where you can see the status of the transfer.

7.  Wait for NSI to send a
    [porcupine](http://www.fishbc.com/adventure/wilderness/animals/porcup.htm),
    which is slightly faster than a turtle, over to the department who
    sends domain transfer confirmation e-mails. As a side note, this
    porcupine was a near friend of the turtle killed in step 4, so it's
    a very unhappy porcupine.

    At the domain transfer confirmation e-mail team, a collection of
    university dropouts who were specially recruited because of their
    unique combination of being unable to write understandable sentences
    while maintaing a high level of legal bullshit, handwrites each
    transfer confirmation mail to make it amazingly hard to understand.

    The general idea seems to be that the reader should be given the
    impression that the only thing that can be done is to cancel the
    transfer, that way keeping the domain at NSI.

    The secret hidden inside the long letter is that the website address
    which is used to cancel the transfer is actually also used to accept
    transfers. So, visit the URL and think twice before clicking on the
    correct button.

    The domain name for this site is not under networksolutions.com.
    Odd.

    Each time a customer accepts a transfer, they kill the messenger
    (i.e., the poor unhappy porcupine).

    I'm feeling bad about killing a porcupine.

8.  Gandi sends a mail about the completion of the domain transfer.

9.  Now, if it's time for renewal, NSI sends a mail where they tell you
    that you can renew the domain that were transferred. I'd guess that
    clicking one of the links in this letter will activate the
    jet-fueled department of incoming transfer, which will re-transfer
    the domain back to NSI in just about 0.2 seconds.

I'm a happier person now, even though I've implicitly killed two turtles
and one porcupine.

