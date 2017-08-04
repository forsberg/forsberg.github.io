---
layout: post
title: 'Hadoop lesson learnt: Restart datanodes after modifying dfs.balance.bandwidthPerSec'
tags: [hadoop]
redirect_from: /blog/archive/2010/09/10/hadoop-balancer-restart-datandoe
---

I was rebalancing one of the Hadoop clusters I run at work. It was not
running very fast, so I modified the appropriate setting:

    <property>
      <!-- 100Mbit/s -->
      <name>dfs.balance.bandwidthPerSec</name>
      <value>104857600</value>
    </property>

I restarted the namenode and thought that would make the trick. But no,
you also need to restart all your datanodes for the setting to take
effect. Now I can see some action on my network graphs :-).

