---
layout: post
title: LVS/IPVS on Openstack - Bad Idea.
---
I'm in the middle of moving a REST API cluster from one datacenter to another at work. This also involves moving off bare metal hosts and onto Openstack virtual machines in an internal Openstack cluster.

For loadbalancing, we're using Linux Virtual Server (LVS) / IPVS (The Linux IP Virtual Server) with keepalived.  This is a pretty ancient solution, but when it comes to loadbalancing TCP connections, it has pretty awesome performance.

But.. how about running it on a virtual machine under openstack? I was a bit sceptical beforehand, and asked our hosting department if there were any other projects using LVS on Openstack - and yes, there were. No problem.

Famous last words.

Turns out that due to openstack configuring a firewall on the physical host (compute node) which handles all connections to virtual machine, LVS on openstack machines does not play well. The connection tracking table on the stateful firewall setup (iptables) will fill up if there's an LVS/IPVS virtual machine getting lot's of connections.

I suspect that the fact that we run this LVS in *Direct Route (DR)* mode doesn't help, as the conntrack code only see one half of the traffic flow - return packets from the worker nodes are sent directly to clients, not via the loadbalancer machine. This is really good for performance, but perhaps means that conntrack code can't detect when TCP connections are shut down? This is just a theory, though.

If you have full control over your machine (i.e run on bare metal) and still want a stateful firewall there are ways to instruct iptables to not use connection tracking for some packets, with the NOTRACK mark on packets in iptables. [Here's some info on that|http://security.maruhn.com/iptables-tutorial/x4772.html] But our hosting department didn't want to do this, as the firewall is handled by openstack. Also, they did not want to raise the limit on the number of connections that the conntrack tables can hold too high, since it's a system shared by multiple tenants.

We're getting a pair of physical machines instead. You live and learn.