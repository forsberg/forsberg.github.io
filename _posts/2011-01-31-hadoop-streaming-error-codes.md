---
layout: post
title: 'Hadoop Streaming Error Codes'
tags: [hadoop]
redirect_from: /blog/archive/2011/01/31/hadoop-streaming-error-codes
---

I'm using Hadoop Streaming a lot. It's exit codes has been something of
a mystery, so today I decided to find out by looking at the source code.

The exit codes are listed in
[StreamJob.java](http://svn.apache.org/viewvc/hadoop/common/branches/branch-0.20/src/contrib/streaming/src/java/org/apache/hadoop/streaming/StreamJob.java?revision=835239&view=markup),
and are as follows:

0.  Success
1.  Job not successful, i.e. something went wrong with M/R code.
2.  Bad input path
3.  Invalid jobconf
4.  Output path already exists
5.  Error launching job. Could be any error, for example some HDFS
    communication error.


