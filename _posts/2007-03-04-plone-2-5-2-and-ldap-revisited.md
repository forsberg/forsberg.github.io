---
layout: post
title: 'Plone 2.5.2 and LDAP - revisited'
tags: [software,LDAP,plone]
redirect_from: /blog/archive/2007/03/04/plone-2-5-2-and-ldap-revisited
---

One or two years ago, I spent some time trying to understand how to
connect Plone 2.0 to LDAP. I really had no luck as things were
complicated. Reading out existing users from the directory might have
been possible, but trying to create users was a thing never heard of.

I decided to check out the current state of Plone and LDAP again with
amore modern version of Plone, in my case, Plone 2.5.2. After some heavy
experimentation, I've come to the conclusion that the software involved
has grown more mature, but it's still hard to get it working.

### Sources of Information

-   [http://plone.org/documentation/how-to/plone-2-5-and-openldap-integration-for-users-and-groups](http://plone.org/documentation/how-to/plone-2-5-and-openldap-integration-for-users-and-groups)
    is *the* source of information in this matter. It's rather long, but
    it's worth reading.
-   [http://thread.gmane.org/gmane.comp.web.zope.plone.user/53770](http://thread.gmane.org/gmane.comp.web.zope.plone.user/53770)
    is a very long thread on the plone-users mailing list, with many
    pieces of information.\
-   [http://article.gmane.org/gmane.comp.web.zope.plone.user/61148](http://article.gmane.org/gmane.comp.web.zope.plone.user/61148)
    is an article that makes some observations on what does work, and
    that doesn't.\
-   Do *NOT* read
    [http://plone.org/documentation/how-to/ldap-authentication-with-plone](http://plone.org/documentation/how-to/ldap-authentication-with-plone)
    - it's only valid for Plone 2.1.

### Software Requirements

-   [python-ldap](http://python-ldap.sf.net). Make sure the python that
    is used to run Zope has this module available, or nothing at all
    will work.
-   [LDAPUserFolder](http://www.dataflake.org/software/ldapuserfolder/).
    I used version 2.8beta. \
-   [LDAPMultiPlugins](http://www.dataflake.org/software/ldapmultiplugins/).
    I first tried version 1.4, but got some problems. Version 1.5,
    released yesterday(!), works much better.
-   The LDAPMultiPlugins patch available at
    http://antiloop.plone.org/LDAPMultiPlugins-plone.org.patch. For me,
    it applied cleanly on top of LDAPMultiPlugins 1.5. It adds
    functionality that is available and needed by PlonePAS. Group
    memberships seems to work much better with this patch than without.
-   Two patches, one on CMFPlone/RegistrationTool.py ([download
    here](../software/patches/CMFPlone-ldapmember.diff "Patch on CMFPlone/RegistrationTool.py to allow user registration with LDAP")),
    and one on
    PasswordResetTool/skins/PasswordReset/registered\_notify\_template.pt
    ([download
    here](../software/patches/passwordresettool-ldapmember.diff "Patch on PasswordResetTool/skins/PasswordReset/registered_notify_template.pt to allow user registration via LDAP")).
    Without these, registration will fail. Please note that both patches
    are ugly hacks that are not long-term solutions to the problem.\
-   This patch:
    [http://www.zope.org/Collectors/PAS/53/plugin-registry-satisfaction.patch](http://www.zope.org/Collectors/PAS/53/plugin-registry-satisfaction.patch),
    or login after password reset will fail with a recursion depth
    error.

### Installation

Drop LDAPUserFolder and LDAPMultiPlugins into your Products folder,
apply patches listed above, and restart Zope.\
\

### Configuration

Follow
[http://plone.org/documentation/how-to/plone-2-5-and-openldap-integration-for-users-and-groups.](http://plone.org/documentation/how-to/plone-2-5-and-openldap-integration-for-users-and-groups.)
In short, you add a LDAP Multi Plugin to your PAS folder (acl\_users in
ZMI) by using the dropdown in the top right corner and then configure
it.\
\

### Theory of Operation\

Plone 2.5 uses PlonePAS, which is an adaption of Zope's PAS (the
Pluggable Authentication System) for its user/group handling. That is a
good thing, as PAS is a very flexible system that can do just about
anything. \
\
To get LDAP users/groups/authentication, LDAPMultiPlugins need to be
installed and configured. After configuration, LDAPMultiPlugins contain
an LDAPUserFolder that is used to actually fetch information from LDAP.
The different plugins in LDAPMultiPlugins then add functionality such as
authentication, user and group enumeration et. al. to PlonePAS.\
\
Configuration of which LDAP server(s) to use, which base to use etc are
made by visiting acl\_users -\> <your LDAPMultiPlugin\> -\> Contents -\>
acl\_users. A bit awkward to find, if you ask me.\
\

### Notes

\
It's very important to pay attention to the LDAP Schema tab under the
LDAPUserFolder.

-   The LDAP attribute used to keep the full name of the user must be
    mapped to fullname. In my case, this means that the LDAP attribute
    *cn* should be mapped to *fullname.* For other directory
    configurations the attribute may be named differently. Novell
    eDirectory for example, uses cn as username.

-   The LDAP attributes used to keep the e-mail address of the user must
    be mapped to email. In most cases this means that the LDAP attribute
    *mail* should be mapped to *email*.
-   Only attributes listed in the LDAP Schema tab are available in the
    dropdowns used to select which field to use as login name attribute,
    username etc in the configuration of LDAPUserFolder. \
-   All attributes listed as MUST in the LDAP schemas used to create new
    users (and search for existing) *must* be listed under the LDAP
    Schema. If not, user registration will fail due to LDAP schema
    errors. \

It's also very important to pay attention to the list of User Object
Classes in the configure tab. This list is used both to construct the
query used when searching for user objects, and to create new user
objects at registration. At new user registration, an LDAP object is
first created with all attributes (except the RDN attribute) set to
[unset] in the LDAP database. As mentioned above, all attributes listed
under the LDAP Schemas tab are filled with this value. Later on in the
registration codepath, the attributes actually mapped to plone
attributes are set (one attribute at a time, in separate LDAP
requests).\
\
The order of the PAS Plugins is very important. To get user registration
to work, and for other things as well, the LDAP Multi Plugin should be
at top of the list of plugins for each type of plugin. \
\
For (much) better performance, add caching by visiting the Caches tab of
both ZMI-\>acl\_users and your LDAP Multi Plugin. Adding a cache to
source\_groups also seems like a good idea (there's no cache tab, so
you'll have to find the URL to the cache management yourself - it's
something like
http://uterus:8080/Plone/acl\_users/source\_groups/ZCacheable\_manage.
For me, it seems to work using the RAM Cache Manager that already exist
in any Plone 2.5 installation. \
\
That's all the things I can remember as being important from yesterday's
late night session :-).\
\


