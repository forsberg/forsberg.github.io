---
layout: post
title: 'Autofs and LDAP'
tags: [software]
redirect_from: /blog/archive/2006/06/27/autofs-and-ldap
---

Today I began working on replacing the NIS installation at work with an
LDAP database.

As I've used the PAM and NSS LDAP modules a lot at customer sites
integrating against eDirectory, I was rather comfortable with that part
of the integration. What I didn't know much about was how the
automounter integrates with LDAP.

It turns out that this was rather easy, although the documentation is
sparse. Also, the fact that I have to cope with the rather old autofs in
Red Hat Linux 7.3 complicated the installation a bit (I have one machine
on the network that must run RHL 7.3. The rest of the machines are
running a variety of modern Linux distributions)

Client Configuration
====================

Instead of having to manually specify which mount points to automount in
*/etc/auto.master* on each client, all configuration is stored in LDAP.
To instruct autofs to read LDAP to find automountpoints, add *ldap* to
the *automount* line in */etc/nsswitch.conf*. In my case, the line looks
like this:

    automount: files ldap

This instructs automount to first check */etc/auto.master* for mount
points, and then search LDAP.

Which LDAP Server is Used?
--------------------------

Autofs has to know which LDAP server to use. It seems the method of
aquiring this information is a bit different on different distributions.
The Red Hat Linux machine read */etc/ldap.conf* which is the
configuration file for nss\_ldap and pam\_ldap, while my Debian sarge
workstation reads */etc/ldap/ldap.conf* which is configuration for the
OpenLDAP libraries. I have yet to see which file is used by Fedora Core
et. al.

It also seems like there's some support for finding which LDAP server
via DNS RR records, but I haven't investigated this further.

Old Autofs - LDAP v2-style bind, but with LDAP v3?
--------------------------------------------------

One problem on the Red Hat Linux 7.3 machine was that it was trying to
do a LDAP version 2-style bind over LDAP version 3. It was trying to
bind as the DN of the ou for an automount map (more about this later),
with a null password. My OpenLDAP didn't like this, expecting either a
regular bind with DN **and** password, or an anonymous bind with null DN
and null password.

I solved this problem by patching autofs. I could probably have upgraded
autofs as well, but I'm not sure autofs 4 works with the current kernel
version, so patching was easier. I still have to include the *allow
bind\_v2* in the server configuration.

Data in LDAP
============

To find which mount points to handle, autofs will search LDAP for
entries with the objectclas *automountMap*. It will then search for all
entries under this DN with the objectclass *automount*, each of them
representing a mount point for the automounter to handle.

Each of the *automount* entries under the *automountMap* entry points to
another container in the LDAP tree, under which you store one
*automount* entry per possible subdirectory to the mount point.

Confused? Let's show some example:

The automountMap and its subtree looks like this:

    dn: ou=auto.master,ou=autofs,dc=example,dc=com
    ou: auto.master
    objectClass: top
    objectClass: automountMap

    dn: cn=/import,ou=auto.master,ou=autofs,dc=example,dc=com
    objectClass: automount
    cn: /import
    automountInformation: ldap:ldap-master.example.com:ou=auto.import,ou=autofs,dc=example,dc=com

    dn: cn=/home,ou=auto.master,ou=autofs,dc=example,dc=com
    objectClass: automount
    cn: /home
    automountInformation: ldap:ldap-master.example.com:ou=auto.home,ou=autofs,dc=example,dc=com

This tells the automounter that it should handle */home*, and that
information about which directories are available to mount under */home*
is available on the LDAP server *ldap-master.example.com* under the DN
*ou=auto.home,ou=autofs,dc=example,dc=com*.

There's similar information for our second automount point, */import*

Now, let's inspect *ou=auto.home,ou=autofs,dc=example,dc=com*

    dn: ou=auto.home,ou=autofs,dc=cendio,dc=se
    ou: auto.home
    objectClass: top
    objectClass: organizationalUnit

    dn: cn=wingel,ou=auto.home,ou=autofs,dc=cendio,dc=se
    cn: wingel
    objectClass: automount
    automountInformation: -rsize=8192,wsize=8192,intr fileserver:/export/home/wingel
    dn: cn=thomas,ou=auto.home,ou=autofs,dc=cendio,dc=se
    cn: thomas
    objectClass: automount
    automountInformation: -rsize=8192,wsize=8192,intr fileserver:/export/home/thomas
    dn: cn=forsberg,ou=auto.home,ou=autofs,dc=cendio,dc=se
    cn: forsberg
    objectClass: automount
    automountInformation:  -rsize=8192,wsize=8192,intr fileserver:/export/home/thomas

As you can see, under the *auto.home* ou, there's one entry for each
possible mount under /home. The *automountInformation* attribute
contains the information the automounter uses to do the actual mount.

