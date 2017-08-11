---
layout: post
title: Setting Fully Qualified Domain Name (FQDN) on Linux
---
There are many ways of setting the fully qualified domain name on a Linux machine. Some set it directly in `/etc/hostname`, something which, after reboot, will make the hostname command return the fqdn:

  # hostname
  host.example.com

This is a bit of the easy and quick fix, and will not necessarily work with all systems. Also, it doesn't work to weel on multi-domain systems.

A better trick that I found while dealing with Openstack hosts that are managed via [cloud-init](https://cloudinit.readthedocs.io) is to set just the hostname in `/etc/hostname`, then add an entry to `/etc/hosts`. It doesn't have to be an entry that points at any real IP address, just as it contains both the FQDN and the hostname. So:

  cat /etc/hosts
  127.0.1.1  hostname.example.com hostname

  cat /etc/hostname
  hostname

This is something I have been struggling with for years, yet the fix is so easy. 
