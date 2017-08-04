---
layout: post
title: 'Migrating Plone Sites to Django'
tags: [software,plone,django,noplone]
redirect_from: /blog/archive/2008/11/01/migrate-plone-to-django
---

As [mentioned earlier](/blog/archive/2008/09/21/bye-plone-hello-django)
on this blog, I have converted this site from [Plone](http://plone.org)
to [Django](http://www.djangoproject.com).

The conversion included migrating most of the data from the Plone
instance's [ZODB](https://launchpad.net/zodb) (Zope Object Database)
into Django's ORM.

The hard part of that process is to get the data out of ZODB as the
format depends completely on which Plone products you have been using.
You need to check the schema for each product for which you want to
extract data to get the field names, and you need to write code for
extracting the data from each type of content type and add a new object
in Django's ORM, translating data from one format to another in some
cases.

In my case, I wrote a script that takes care of:

-   Document and Folder objects from Plone's standard contenttypes.

-   Blog entries in a Quills blog.

The script will traverse all Document, Folder and Blog entries and
extract their data, adding instances of Django models from two custom
Django products I have written.

A second script will then read the data from Django's database and
modify the URLs in <img\> tags, downloading the images from the Plone
site via HTTP to a directory which will be configured as MEDIA\_ROOT in
Django. The script does the same for <a\> tags that refer to images,
.tar.gz files, etc. that also were stored in the ZODB of the Plone
instance.

Each site that wants to do a conversion from Plone to Django will have
to write their own script, as the set of products used in the Plone
instance is site-specific, and the set of applications used in Django is
also site-specific. However, I have made my conversion scripts available
via subversion in the hope that they can serve as an example.

To access the scripts, either check them out with your subversion
client. Example:

    git clone git://github.com/forsberg/misctools.git

The scripts are in the plone2django\_migration subdirectory.

You can also browse them here:

[](https://github.com/forsberg/misctools/tree/master/plone2django_migration)

