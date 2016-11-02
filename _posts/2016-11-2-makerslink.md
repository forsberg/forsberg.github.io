---
layout: post
title: An evening at MakersLink
---

Today I've spent a couple of hours at [MakersLink](http://www.makerslink.se). I have a couple of [MySensors](http://www.mysensors.org) sensors at home, but it's been a long time since I had time to deal with it. So today I'm starting off what I hope will be a weekly activity - an evening at the makerspace to get some stuff done.

Today was mostly about trying to figure out how to make the rain sensor I've built work. I have assembled it and tried to use the example [RainGauge Sketch](https://www.mysensors.org/build/rain), but that sketch really is not made for being run on battery - it drained my LiPo in two days.

So today I spent some time trying to figure out if the sketch can be modified to run on battery, with the [sleep function](https://www.mysensors.org/download/sensor_api_20#sleeping), but the problem is that when you sleep using that function (which uses an watchdog interrupt to really shut down the arduino), the millis() function in arduino stops updating. Meh.

So I tried just faking the number of milliseconds by adding to variable the same number of milliseconds as I would sleep, with the thinking that I can sync from the mysensors controller now and then.

*No* - that's just wildly inaccurate.

So, that seems rather impossible. So I think I'll revert to making the sensor rather stupid, reporting only when there's new rain, and then do the work in the controller instead. This will require me to do some [Home Assistant](http://home-assistant.io) hacking, something I've been thinking about doing for a long time anyway.

Speaking of long times, this is the first in what I hope will be a series of blog entries about various things. This Jekyll thing seems convenient.