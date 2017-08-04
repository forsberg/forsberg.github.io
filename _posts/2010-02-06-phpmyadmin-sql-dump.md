---
layout: post
title: 'Backup of MySQL via phpMyAdmin'
tags: [misctools,python]
redirect_from: /blog/archive/2010/02/06/phpmyadmin-sql-dump
---

My girlfriend runs a blog on a cheap hosting firm that doesn't provide
any way of doing proper SQL dumps of the MySQL database used by the
blogging software.

There are plugins for [Wordpress](http://wordpress.org/) that can do
full backups, but I prefer doing raw SQL dumps + a filesystem backup.
That way, you know what you get, you don't have to trust the backup
plugin author to do it right.

The hosting firm does provide access to a
[phpMyAdmin](http://www.phpmyadmin.net/) installation which you can use
to download SQL dumps. The trick is of course to do this automatically,
as good backups need to be unattended.

I wrote a python program that can do this, using what turned out to be
an excellent library for programmatic web browsing:
[mechanize](http://wwwsearch.sourceforge.net/mechanize/).

The backup script is available in my [misctools
project](http://github.com/forsberg/misctools/tree/master/phpmysqladmin_backup)
on [GitHub](http://github.com).

