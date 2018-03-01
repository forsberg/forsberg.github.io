---
layout: post
title: Let's Encrypt - connection timeout 
---
Had a problem with the letsencrypt certificate used to secure my [Home Assistant](http://home-assistant.io) 
computer at home. It was not renewing.

I did get a couple of warning e-mails, which I ignored, and then noticed I could no longer connect to home assistant. There was no good error message from the Home Assistant web frontend (which is all javascript magic), but trying to connect with `curl` from the Linux command line, the error was very clear.

Now, I tried rerunning the `certbot` command manually. It bailed out with an error message about letsencrypt servrs being unable to connect to my domain name via http to verify ownership. 

So that's where I had my first [D'oh](https://www.youtube.com/watch?v=H22t-tiWiLw) moment: I had forwarded port 80 on my router (which I fiddled with a while back), only 443.

However, fixing that did not fix the problem, even though I confirmed I could now reach the domain name via http from the internet.

The domain name had both an *A* and an *AAAA* entry, since I had it connected to IPv6 via an [he.net](http://he.net) tunnel, but I had to disable the tunnel due to problems using Netflix, which would stupidly think I was trying to circumvent their geoblocking. So there was an IPv6 address published, but it would timeout - and that caused the whole letsencrypt verification to fail. Meh.

Removed AAAA entry, waited a few minutes, reran `certbot` - problem fixed.
