---
layout: post
title: 'QNAP TS-109 II - First Impressions'
tags: [linux,review,ipv6,turbostation]
redirect_from: /blog/archive/2008/12/02/qnap-ts-109-ii-first-impressions
---

I bought a second hand
[Squeezebox](http://www.slimdevices.com/pi_squeezebox.html) the other
day. The Squeezebox must read its files from a server running
Squeezecenter, and since I don't want my workstation running all day
(it's consuming energy. I'm trying to be environmentally friendly when I
can), I had to find a low-power alternative.

I have been thinking about getting some kind of server running at home
for a while. There are other things I want it to do as well:

-   Keep a [SixXS](http://www.sixxs.net) IPv6 tunnel up, and route an
    IPv6 subnet for home.
-   Be able to Wake-on-LAN my main workstation.
-   Get better network throughput than from my stupid 3com NAT box.
-   Etc, etc..

After some consideration, I bought a [QNAP TS-109
II](http://www.qnap.com/pro_detail_feature.asp?p_id=91). It has a 500MHz
ARM processor, 256Mb of RAM and consumes 14Watts of energy when active,
6,6W when not. That's quite OK. I bought a [WD Caviar Green
500Gb](http://www.wdc.com/en/products/products.asp?DriveID=338) hard
drive for it. That drive is supposed to be quiet and energy efficient.

Another killer fact about the QNAP is that the upcoming [Debian
Lenny](http://www.debian.org/releases/lenny/) will have official support
for all TurboStation models from QNAP. It's even [listed as a press
release on QNAP's
webpage](http://www.qnap.com/PressRelease_detail.asp?pr_id=109). The
installation link from the press release doesn't seem to work anymore,
though. The [Debian on QNAP TS-109
pages](http://www.cyrius.com/debian/orion/qnap/ts-109/index.html) are
very helpful, though.

The QNAP + hard drive arrived today, and I unpacked and assembled the
two (very easy), plugged it in, found its IP address from the list of
DHCP entries in my NAT box, and tried to connect to it via a web browser
on both port 80 and port 8080.

Unfortunately, I was met by a message in several languages basically
telling me that "This box is not initialized, do what the manual says".
And the manual says that you need a Windows computer to initialize the
TS-109.

**Doh!**

**I don't own a Windows computer!**

Fortunately, my girlfriend has an XP box which I could use to run the
"QNAP Finder" to install the QNAP. Still, I find this irritating.
There's support for Mac as well, but I don't have any Mac neither.

I'm sure there's some way of initializing the device without Windows,
but that might require lot's of knowledge on the RPC protocol used to
talk to the device. Presumably, it's some kind of RPC over HTTP, as the
only ports the device has open at initial startup is 80 and 8080.

Navigating around in the menus for a while, I was not surprised to see
that running Debian on the machine would be the best option for me.
Specifically:

-   There's no support for NFS on the TS-109 II. You need the TS-109 II
    *Pro* for that.
-   There's no network routing support in the standard firmware, and
    that's not surprising - this is a NAS box afterall. But with Linux
    and it's VLAN support and iptables, it *should* work well. We'll see
    about that... :-)
-   The configuration can't be easily handled via
    [Puppet](http://reductivelabs.com/trac/puppet) when running the
    standard firmware. That's something I do for other servers I manage.

Anyway, I think I'll be happy with this box. I might add an external
eSATA enclosure later to provide backup of the stuff I keep on the QNAP.
We'll see. Backing up stuff to [Amazon S3](http://aws.amazon.com/s3/) is
another option.

