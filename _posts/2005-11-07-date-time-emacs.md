---
title: Date and time in Emacs status bar
layout: post
redirect_from:
---

Emacs is a very good editor (Well, almost religion for some people :-) ), with so much configuration possibilities one could configure it for years, and that's good !

I want emacs to display the current date and time in it's status bar, place this in your `$HOME/.emacs` and start emacs..

    (setq display-time-day-and-date t
       display-time-24hr-format t)
    (display-time)

And watch the magic ! It'll now display Date, Time, system load and mail status in the status bar. Really useful, if you ask me.
