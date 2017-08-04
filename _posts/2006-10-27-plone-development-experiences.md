---
layout: post
title: 'Plone Development Experiences'
tags: [plone]
redirect_from: /blog/archive/2006/10/27/plone-development-experiences
---

For the last days, I've been doing some heavy Plone development for a
community site that hopefully will be launched sometime during the next
few days. Although I have done a fair amount of Plone development
earlier, this time, I did learn a lot, especially about ArchGenXML.

Content Types
=============

When I first started using Plone, I had trouble understanding the
concept of "content types". All the documentation was talking about
content types. Everybody was speaking about them, but I didn't want
content types, I just wanted some scripts to create some users in an
LDAP database. I ended up tacking ZPT files to existing content types.
Ugly and very hackish.

Now, I think I've understood the concept. In Plone, all content is an
instance of a content type. You need a page creating users in an LDAP
database? It's a CreateUsersPage Content Type! That's how to do it with
Plone. At least that's my current understanding.

For this project however, the idea of content types was very easy to
apply to the problem. The community wants to build a database of
applications that work in a specific environment (I'm a bit secretive on
this project since it's not set in production yet) - that's a perfect
match. Each application in the database is modelled as an
AppDBApplication content type. There's AppDBCategory objects, and last
but not least, the AppDB content type which holds AppDBCategory and
AppDBApplication objects.

Working with ArchGenXML
=======================

[ArchGenXML](http://plone.org/products/archgenxml) is a code generator
for Plone, or more specifically for Archetypes-based content types.
Archetypes is the framework for creating content types that is used in
Plone, at least in recent versions.

Basically, you create an UML diagram using some UML editor such as
[ArgoUML](http://argouml.tigris.org).
[ArchGenXML](http://plone.org/products/archgenxml) then generates code
based on the information in the UML diagram. This sounds complicated,
and it has a somewhat steep learning curve, but once you get it, it's a
very productive way to create Plone *Products* - A *Product* is another
Plone concept. It's something you install in your Plone instance which
keeps a bunch of related code together, for example some content types
and their ZPT templates and some tools used by the content types
together with for example custom workflows.

[ArchGenXML](http://plone.org/products/archgenxml) generates all the
boilerplate needed to create a product, including code to interact with
the product installer inside Plone. Very handy.

If you haven't done so already, you really need to read the [ArchGenXML
tutorial](http://plone.org/documentation/tutorial/archgenxml-getting-started)

In this project, I created a class in the UML diagram for each type of
content so there was one AppDB class, one AppDBApplication class and one
AppDBCategory class. The AppDBApplication and AppDBCategory classes were
then *Associated* (an UML term) with AppDB, which automatically makes
AppDB a folder class that can hold objects of AppDBCategory and
AppDBApplication.

Each class is then equipped with attributes and operations. The
attributes end up as automatically generated input forms and
automatically generated renderings of the data in the end. This is very
handy! In my AppDBApplication for example, I added an attribute called
'version' for storing the version of the piece of software that each
object in the database refers to. After generating the code with
ArchGenXML, I end up with an Archetypes class that automatically creates
an input form where for the version attribute, as well as an
automatically generated page for viewing all the data, where the version
field is included.

Customizing View and Edit Templates
===================================

Another thing I understood just recently was how you are supposed to
edit the view and edit pages for Archetypes-based content types in a
decent way. The HOWTO named [How to Customize View or Edit on Archetypes
Content
Items](http://plone.org/documentation/how-to/how-to-customise-view-or-edit-on-archetypes-content-items/view?searchterm=base_view)
is really a *must read*!

Using the templates in the HOWTO as a basis for your view and edit forms
makes Archetypes development much easier since it takes care of some of
the fuzz, such as making sure there are relevant variables already
defined in your template.

Make sure you read the whole HOWTO, including its comments. There is one
real goodie in one of the comments - the basis for how to create edit
forms that don't look like all other edit forms in Archetypes. Here's
how you do it:

1)  Create a new filesystem template named
    <nameofyourcontenttype\>\_edit.pt. Place it in the skins folder of
    your product. Use the edit template in the HOWTO as base, or use
    this stripped-down version:

    >     <html xmlns="http://www.w3.org/1999/xhtml"
    >           xml:lang="en"
    >           lang="en"
    >           xmlns:tal="http://xml.zope.org/namespaces/tal"
    >           xmlns:metal="http://xml.zope.org/namespaces/metal"
    >           xmlns:i18n="http://xml.zope.org/namespaces/i18n"
    >           i18n:domain="plone">
    >
    >       <metal:head define-macro="topslot">
    >       </metal:head>
    >
    >       <metal:head define-macro="javascript_head">
    >       </metal:head>
    >
    >       <body>
    >             <!-- body, editform , fields, buttons, the default macro 
    >                  contains a number of slots which usually provide enough
    >                  ways to customise so often I use that macro and just 
    >                  fill the slots
    >             -->
    >             <metal:body define-macro="body">
    >                 <metal:default_body use-macro="here/edit_macros/macros/body">
    >
    >                   <metal:block fill-slot="widgets">
    >                   <!-- This is where you'll add widgets -->
    >                   </metal:block>
    >
    >                 </metal:default_body>
    >             </metal:body>
    >
    >       </body>
    >
    >     </html>

2)  Inside the *<metal:block fill-slot="widgets"\>* tags, add one of
    these for each field in your schema that you want to appear in the
    edit forms:

<!-- -->

    <metal:fieldMacro use-macro="python:here.widget(<name of your field>, mode='edit')

Of course, replace *<name of your field\>* with the name of the fields
for which you want the input field to appear, as defined in the schema
of your archetype class. You are free to use any html elements and css
to position the widgets where you want them.

Customizing Widgets
===================

In this project, I wanted some javascript to be triggered when one of
the input fields is modified. It's a simple thing - I want some other
input fields to enabled or disabled based on the value of the first
input field (a radio button collection with two alternatives).

I had no idea on how to accomplish this, so I asked on the \#archetypes
IRC channel on freenode. The trick is to copy the ZPT template used to
display the widget you are using to your own skins directory, naming it
appropriately, then using the macro attribute on the widget in the
archetypes schema, point to the new template. An example:

*) I have a field named*operatingsystem\* in my archetypes
  ~ schema. It's defined as follows:

        StringField(
             name='operatingsystem',
             widget=SelectionWidget(
                 label="Written for",
                 description="The operating system the application originally was written for",
                 macro="appdb_widgets/appdbapplication_selection",
                 label_msgid='AppDB_label_operatingsystem',
                 description_msgid='AppDB_help_operatingsystem',
                 i18n_domain='AppDB',
             ),
             vocabulary=NamedVocabulary("""operatingsystem""")
         ),

    I'm using
    [ATVocabularyManager](http://plone.org/products/atvocabularymanager)
    in this project, hence the *NamedVocabulary* as vocabulary.

    Note the line *macro=appdb\_widgets/appdbapplication\_selection*.

*) Since the field is using a*SelectionWidget*, I copied*selection.pt\*
from *<instance home\>/Products/Archetypes/skins/archetypes/widgets*
into the
  ~ directory *appdb\_widgets* in the skins dir for my product and named
    the copied file *appdbapplication\_selection.pt*.

    Note: *Do not* call the subdirectory in your skins dir *widgets*,
    since that will most likely give you an error because Plone will
    then try to find template files for other widgets in your skins
    directory, where they will not be available. This has to do with the
    search order in the plone skins tool.

*) Now edit*appdb\_widgets/appdbapplication\_selection.pt\* and add the
  ~ call to a javascript function.



