---
layout: post
title: 'The XDG Menu Standard Parsers in KDE and Gnome'
tags: [general]
redirect_from: /blog/archive/2006/01/07/the-xdg-menu-standard-parsers-in-kde-and-gnome
---

The XDG Menu parser in KDE is, in at least one respect, much more
forgiving, than the one in Gnome.

Given an example menu file:

    <Menu>
     <Name>YYXXZZ</Name>
     <Directory>/absolute/path/to/directory/file.desktop</Directory>
     ...
    </Menu>

..KDE will happily use it as a Directory file, i.e. a file which
describes a submenu rather than an application, even though the file is
incorrectly named, and even though the filenames inside *<Directory\>*
tags are supposed to be relative according to [the
standard](http://standards.freedesktop.org/menu-spec/latest/).

Gnome 2.10 on the other hand, will freeze in a 99% CPU-consuming endless
loop. 2.12 behaves better, but still won't use the desktop file, instead
showing the *YYXXZZ*, i.e. the name in the *<Name\>* tag, as name of the
menu.

If the desktop file is given as a [Relative
Path](http://standards.freedesktop.org/menu-spec/latest/go01.html),
**and** has a name that ends in .directory, **and** has a
*Type=Directory* line, then it is used by Gnome.

KDE is, in this case, better at following Postel's Law - "be liberal in
what you accept and conservative in what you put out".

My Job is varied. Today I was reading the source code of
[Gnome](http://www.gnome.org). Last week, I was reading the source code
of [KDE](http://www.kde.org). Personally, I run neither, but just a
plain [Sawfish](http://sawmill.sf.net).

