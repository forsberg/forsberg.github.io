---
layout: post
title: 'Installing Ubuntu on a machine with no CDROM drive'
tags: [software,linux]
redirect_from: /blog/archive/2006/11/29/installing-ubuntu-on-a-machine-with-no-cdrom-drive
---

Today I had to install Ubuntu on one of the older machines in the
computer room. It's a 1U server without CDROM drive.

Ubuntu doesn't seem to ship any floppy images. It does ship a utility to
boot from IDE CDROM drives in the case where the BIOS is too old or full
of bugs preventing it to boot from the CDROM. You can do that by
creating a floppy that has drivers for the CDROM and allows booting from
the CD. To be specific, the image shipped with the CD contains
Smartbootfloppy which has a webpage (sort of) at
[http://btmgr.sourceforge.net/](http://btmgr.sourceforge.net/)\

However, since this machine had no CD at all, this didn't solve the
problem.

My initial thought was to try using a CDROM drive connected to the USB
port (at least the machine is new enough to have two USB ports). This
however proved impossible due to the BIOS lacking functionality to
recognize and boot from USB CDROM drives. And the boot manager from
Ubuntu doesn't recognize USB drives either. Dead end.\

I did some research on this, and found several places where people were
asking how to do, but no places where people actually got good answers.
\

The solution to my problem was to create a boot floppy with etherboot. I
went to [http://www.rom-o-matic.net](http://www.rom-o-matic.net) and
located my network card in the dropdown. I was lucky enough to know the
exact PCI ID numbers of the network card which helped in finding the
correct driver. If you don't know, try to locate the card by name in the
list. Opt for a bootable floppy image, download it and then write it to
a floppy per the instructions on the site.\
\
You then need to configure a tftp server on another machine on the same
network. The server should be configured to serve the contents of
*/install/netboot* directory of the Ubuntu CD as root directory. This
way, when the computer you are about to install asks for the file
*pxelinux.0,* the *pxelinux.0* in */install/netboot* on the Ubuntu CD
will be served.\
\
I did this by installing the atftpd package, mounted my ubuntu CD on
*/media/cdrom* and added */media/cdrom/install/netboot* as commandline
argument to in.tftpd in /etc/inetd.conf. Don't forget to restart inetd
after doing this.\
\
I then configured my DHCP server as follows:\
\

    host tobeinstalled {        hardware ethernet 00:80:C8:F8:51:25;                next-server myinstallhost;        filename "pxelinux.0";        allow bootp;        allow booting;}       

This will make dhcpd tell the client that it should ask *myinstallhost*
for *pxelinux.0* at boot.\
\
Inserted the floppy in the computer to be installed and rebooted it. It
downloaded a bunch of files via TFTP, and then gave me the regular
Ubuntu install prompt. Yay!\
\


