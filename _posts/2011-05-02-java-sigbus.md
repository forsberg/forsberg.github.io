---
layout: post
title: 'Java SIGBUS - an unclear way of saying /tmp is full'
tags: [linux,java]
redirect_from: /blog/archive/2011/05/02/java-sigbus
---

I had the following happen for every new java process on one of my
servers the other day:

    server:~$ java
    #
    # A fatal error has been detected by the Java Runtime Environment:
    #
    #  SIGBUS (0x7) at pc=0x00007f3e0c5aad9b, pid=17280, tid=139904457242368
    #
    # JRE version: 6.0_24-b07
    # Java VM: Java HotSpot(TM) 64-Bit Server VM (19.1-b02 mixed mode linux-amd64 compressed oops) 
    # Problematic frame:
    # C  [libc.so.6+0x7ed9b]  memset+0xa5b
    #
    # An error report file with more information is saved as:
    # /home/user/hs_err_pid17280.log
    Segmentation fault

Turns out this is Java's way of telling you that the /tmp directory is
full. It's trying to mmap some performance/hotspot-related file in /tmp
which succeeds, but when it's trying to access this area, it will get
the SIGBUS signal.

More info
[here](http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=6563308)

