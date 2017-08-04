---
layout: post
title: 'OpenLDAP - loglevel none'
tags: [LDAP]
redirect_from: /blog/archive/2008/05/05/openldap-loglevel
---

For a long time, I have wanted to know which loglevel to set in
OpenLDAP's slapd.conf to get just errors in the log. For many years, I
have obviously been too quick in reading the manual page slapd.conf(5).

The answer is *loglevel none*, which I find less than obvious..\

Today, I also learned that if the LDAP Users and Groups module in Webmin
says *No structuralObjectClass operational attribute*, that may mean
that you're trying to add an object with two structural object classes
set.\


