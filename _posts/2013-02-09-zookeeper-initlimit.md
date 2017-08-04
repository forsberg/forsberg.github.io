---
layout: post
title: 'ZooKeeper failing to elect leader due to initLimit being too small'
tags: [zookeeper]
redirect_from: /blog/archive/2013/02/09/zookeeper-initlimit
---

At [work](http://www.opera.com), I use [Apache
ZooKeeper](http://zookeeper.apache.org/) to coordinate a distributed
service. I find ZooKeeper very easy to work with and program against,
but as all software, it can be troublesome now and then.

I have a 3-node ZooKeeper cluster that was behaving very oddly the other
day. It started with one of the nodes going down due to hardware
trouble. This is supposed to be no problem since 2/3 nodes are still up
and form a quorum. However, the whole service stopped serving clients.

At the time the node that went down crashed, it was the LEADING node of
the cluster, with server id being 3. This meant another node needed to
be elected as LEADER. The node with server id=2 was elected as leader,
but failed to successfully establish leadership with a rather confusing
error message in the log (*/var/log/zookeeper/zookeeper.log*):

    2013-02-07 01:42:09,336 - INFO  [QuorumPeer:/0:0:0:0:0:0:0:0:2181:QuorumPeer@655] - LEADING
    2013-02-07 01:42:09,336 - INFO  [QuorumPeer:/0:0:0:0:0:0:0:0:2181:ZooKeeperServer@154] - Created server with tickTime 2000 minSessionTimeout 4000 maxSessionTimeout 40000 datadir /var/zookeeper/version-2 snapdir /var/zookeeper/version-2
    2013-02-07 01:42:09,342 - INFO  [QuorumPeer:/0:0:0:0:0:0:0:0:2181:FileSnap@82] - Reading snapshot /var/zookeeper/version-2/snapshot.70028d3e5
    2013-02-07 01:42:13,407 - INFO  [QuorumPeer:/0:0:0:0:0:0:0:0:2181:FileTxnSnapLog@256] - Snapshotting: 70028d3e5
    2013-02-07 01:42:23,864 - INFO  [LearnerHandler-/10.20.46.90:32845:LearnerHandler@249] - Follower sid: 1 : info : org.apache.zookeeper.server.quorum.QuorumPeer$QuorumServer@7ab2c6a6
    2013-02-07 01:42:23,865 - INFO  [LearnerHandler-/10.20.46.90:32845:LearnerHandler@273] - Synchronizing with Follower sid: 1 maxCommittedLog =0 minCommittedLog = 0 peerLastZxid = 70028d3cb
    2013-02-07 01:42:23,865 - INFO  [LearnerHandler-/10.20.46.90:32845:LearnerHandler@357] - Sending snapshot last zxid of peer is 0x70028d3cb  zxid of leader is 0x800000000sent zxid of db as 0x70028d3e5
    2013-02-07 01:42:47,691 - INFO  [QuorumPeer:/0:0:0:0:0:0:0:0:2181:Leader@413] - Shutdown called
    java.lang.Exception: shutdown Leader! reason: Waiting for a quorum of followers, only synced with: 2: 
            at org.apache.zookeeper.server.quorum.Leader.shutdown(Leader.java:413)
            at org.apache.zookeeper.server.quorum.Leader.lead(Leader.java:319)
            at org.apache.zookeeper.server.quorum.QuorumPeer.run(QuorumPeer.java:658)

Tried googling on this, but didn't get any helpful hits. I tried all
kinds of tricks to get the service up, then started looking into the
source code, especially the lines that are mentioned in the exception
message.

Turns out I had a misconfiguration. In */etc/zookeeper/zoo.cfg* there's
a parameter *initLimit* described as follows:

    # The number of ticks that the initial 
    # synchronization phase can take
    initLimit=10

In my setup, I had the default value (10) set for this parameter.
Looking at the administrator's guide for the version of zookeeper I'm
running, it describes initLimit as follows:

*"Amount of time, in ticks (see tickTime), to allow followers to connect
and sync to a leader. Increased this value as needed, if the amount of
data managed by ZooKeeper is large."*

That particular ZooKeeper cluster has several hundred thousand objects,
with a database size of roughly 150MiB. I guess that is counted as a
large amount of data in ZooKeeper.

I increased my initLimit to 100, which made the problem go away, the
server started fine and my cluster was able to go into a healthy state
and start serving data again.

What happened here was that the server that was being elected as leader
(with server id 2) was elected leader. It started sending a snapshot of
the database to its follower (with server id 1), but before that
completed and the follower reported itself as ready and following, the
initLimit timeout was reached, and the leader thread decided it had to
give up, since it was only synced with server id 2 (itself). So
increasing initLimit to a value that allowed the snapshot transfer to
complete fixed this problem.

