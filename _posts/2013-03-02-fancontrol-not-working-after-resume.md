---
layout: post
title: 'Fancontrol not working after resume on Ubuntu'
tags: [linux]
redirect_from: /blog/archive/2013/03/02/fancontrol-not-working-after-resume
---

Bought a new computer. Had some trouble with the fan controller built
into the chassis, so got a couple of PWM fans instead since the
motherboard can control 1 CPU and 3 chassis PWM fans.

The BIOS however was a bit limited when it came to how slow you could
make the fan run. So turned to the fancontrol package in ubuntu, and
after some fiddling it worked as intended, even turning off the case fan
when the temperature was below the configured threshold.

However, after suspending then resuming, the fan would go at 100% again,
and not spin down. There's a [launchpad
bug](https://bugs.launchpad.net/ubuntu/+source/lm-sensors-3/+bug/489596)
that tells me I'm not the only one with this problem.

Here's a workaround. Create */etc/pm/sleep.d/20\_fancontrol* with the
following contents:

    #!/bin/sh

    case "${1}" in
        resume|thaw)
      /usr/sbin/service fancontrol restart
      ;;
    esac

This will restart the fancontrol service after resume, which solves the
problem. The fan will run at 100% for a little while at resume, since it
takes a couple of seconds before this script is being run.

