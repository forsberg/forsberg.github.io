---
layout: post
title: Moving to github pages
---

My webpages started out running [Plone](http://plone.org), and I think it was on some old machine I kept running somewhere.

Later on, I moved to a site I wrote myself based on [Django](http://www.djangoproject.com). This is a mistake many have done - writing your own CMS in the hope that it will be useful. There are always others that can do that for you in a better way, and with more resources. The most annoying thing with this site has been that writing content is done in reStructured text (which is OK), but in a small textbox in an admin UI. Not so userfriendly. Also, it's costing me some $20 every month as I'm running it on a rackspace virtualmachine. 

As I often feel that I *want* to write something down, especially when it comes to technical stuff I do at work, I decided to do something about this. And nowadays, there are many fantastic free alternatives. The one I ended up with was [Github Pages](https://pages.github.com) powered by [Jekyll](https://jekyllrb.com). Basically, you create a specially named git repository at github, then push markdown-formatted (Actually, it supports a [whole bunch](https://jekyllrb.com/docs/plugins/#converters-1) of formats, but Markdown is the default one) text files to the git repository, and github will automatically build it into static pages which are served via github's infrastructure.

Very userfriendly. For this user. Also, very cheap.

In the hope that there may be others that have an old, Django-powered, custom CMS that they don't remember how to convert, here's how I converted mine:

    #!/usr/bin/env python
    
    import os
    import sys
    import subprocess
    import codecs
    sys.path = ['/opt/django-sites/efod_se', '/usr/lib/python2.7', '/usr/lib/python2.7/plat-linux2', '/usr/lib/python2.7/lib-tk', '/usr/lib/python2.7/lib-old', '/usr/lib/python2.7/lib-dynload', '/usr/local/lib/python2.7/dist-packages', '/usr/lib/python2.7/dist-packages', '/usr/lib/python2.7/dist-packages/PIL', '/usr/lib/pymodules/python2.7', '/opt/django-sites/', '/opt/django/1.0/lib/python2.5/site-packages']
    
    from efod_se import TYPE_HTML, TYPE_REST, PUBLISHED_STATUS
    from efod_se.efodblog.models import BlogEntry
    
    
    for entry in BlogEntry.objects.all():
        print entry.status == PUBLISHED_STATUS, entry
        if entry.status != PUBLISHED_STATUS:
            print >> sys.stderr, "%s not published, skipping" % entry
            continue
        
        publish_date = entry.publish_date.strftime("%Y-%m-%d")
    
        informat = "rst"
        if entry.contenttype == TYPE_HTML:
            informat = "html"
    
        p = subprocess.Popen(["/usr/bin/pandoc", "-f", informat, "-t", "markdown"],
                             stdin=subprocess.PIPE, stdout=subprocess.PIPE, env=os.environ)
        (stdout, stderr) = p.communicate(entry.content.encode("utf-8"))
    
        content = stdout.decode("utf-8")
        content = content.replace("MEDIA_URL", "/images/django2jekyll")
        
        with codecs.open("/tmp/blogentries/%s-%s.md" % (publish_date, entry.slug), 'w', 'utf-8') as output:
            output.write("""---
    layout: post
    title: '%(title)s'
    tags: [%(tags)s]
    redirect_from: %(redirectfrom)s
    ---
    
    %(content)s
    """ % {"title": entry.title.replace("'", "''"),
           "tags": u",".join(tag.tag for tag in entry.tags.all()),
           "redirectfrom": entry.get_absolute_url(),
           "content": content})
    

Note: The **DJANGO_SETTINGS_MODULE** environment should be set to the python module name that contains django settings. 