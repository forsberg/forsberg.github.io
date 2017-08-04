---
layout: post
title: 'A contenttype template in ZopeSkel''s localcommands'
tags: [software,plone]
redirect_from: /blog/archive/2007/12/02/a-contenttype-template-in-zopeskels-localcommands
---

As [Tarek
noted](http://tarekziade.wordpress.com/2007/11/30/using-zopeskel-to-raise-plone-projects-quality/)
the other day, I've added a template for injecting content types into an
existing Archetype product, using [Mustap's\
localcommands support for
ZopeSkel](http://www.mustap.com/pythonzone_post_234_zopeskel-with-local-commands).
\

Overview
--------

Here's what the contenttype template will do for you after you've
answered some questions:\
\

-   Define a new Add Permission the product's*config.py*
-   Define an interface for the content type you're creating.
-   Create a content type class, in a subdirectory named *content/*
-   Register this content type class in *content/configure.zcml*
-   Register the new content type in the factorytool, by adding to
    *profiles/default/factorytool.xml*
-   Register basic permissions for the new content types, by adding to
    *profiles/default/rolemap.xml*
-   Register the content type with portal\_types by adding to
    *profiles/default/types.xml*
-   Add a new file with configuration information in
    *profiles/default/types/.*\

Example
-------

\
Here's an example on how to use the template. You'll need mustap's
branch of ZopeSkel for this to work:\
\
https://svn.plone.org/svn/collective/ZopeSkel/branches/mustap\
\
Begin by creating a new product based on ZopeSkel's the Archetype
template:\
\

    $ paster create -t archetypeSelected and implied templates:  ZopeSkel#basic_namespace  A project with a namespace package  ZopeSkel#plone            A Plone project  ZopeSkel#archetype        A Plone project that uses ArchetypesEnter project name: efod.testVariables:  egg:      efod.test  package:  efodtest  project:  efod.testEnter title (The title of the project) ['Plone Example']: Contenttype ExampleEnter namespace_package (Namespace package (like plone)) ['plone']: efodEnter package (The package contained namespace package (like example)) ['example']: testEnter zope2product (Are you creating a Zope 2 Product?) [False]: TrueEnter version (Version) ['0.1']: Enter description (One-line description of the package) ['']: Enter long_description (Multi-line description (in reST)) ['']: Enter author (Author name) ['Plone Foundation']: Enter author_email (Author email) ['nospamplease@example.com']: Enter keywords (Space-separated keywords/tags) ['']: Enter url (URL of homepage) ['http://svn.plone.org/svn/plone/plone.example']: Enter license_name (License name) ['GPL']: Enter zip_safe (True/False: if the package can be distributed as a .zip file) [False]: ...

\
Now go into the directory just created:\
\

    $ cd efod.test$ paster addcontent contenttypeEnter contenttype_name (Content type name ) ['Example Type']: Enter contenttype_description (Content type description ) ['Description of the Example Type']: Enter folderish (True/False: Content type is Folderish ) [False]: Enter global_allow (True/False: Globally addable ) [True]: Enter allow_discussion (True/False: Allow discussion ) [False]:   Inserting from config.py_insert into /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/config.py  Recursing into content    Copying +content_class_filename+.py_tmpl to /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/content/exampletype.py    Inserting from configure.zcml_insert into /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/content/configure.zcml  Inserting from interfaces.py_insert into /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/interfaces.py  Recursing into profiles    Recursing into default      Inserting from factorytool.xml_insert into /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/profiles/default/factorytool.xml      Copying rolemap.xml_insert to /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/profiles/default/rolemap.xml      Recursing into types        Copying +types_xml_filename+.xml_tmpl to /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/profiles/default/types/Example_Type.xml      Inserting from types.xml_insert into /home/forsberg/dev/plone/mustaptest/src/efod.test/efod/test/profiles/default/types.xml

\
That's it! After registering the archetype product in your buildout and
installing it in Plone, you'll be able to add new 'Example Type'
content. \
\
Of course, for your custom content type to be really useful, you'll have
to edit it, adding new fields and modifying templates.\
\

Some Details
------------

\
I am by no means a Plone guru, so some of the details in how this
template constructs the new content type may be less than optimal.
Please tell me if that's the case, and I'll see what I can\
do. \

### Base Classes

Depending on the answer to the "Folderish" question, the newly created
content type will inherit either from
Products.ATContentTypes.content.base, or from
Products.ATContentTypes.content.folder. \
\

### Standard Fields\

The template will set up AnnotationStorage and bridge properties for the
standard title and description fields. \

### Security

The Manager role is given the add permission for the content type (in
profiles/Default/rolemap.xml). \
\
zope2.View is required to view the content, and cmf.ModifyPortalContent
to edit.\

### Views\

The standard views auto-generated by Archetypes are used as a default.
Perhaps generating a custom view class, with template, would\
be more Plone3? On the other hand there's already another template for
creating a view available.\

Please test!\
-------------

Please test the template and tell me what you think! What should be made
different, and what have I forgotten?\
\


