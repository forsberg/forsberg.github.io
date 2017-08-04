---
layout: post
title: 'ZSI vs. SugarCRM, 1-0'
tags: [software,sugarcrm,soap]
redirect_from: /blog/archive/2006/09/13/zsi-vs-sugarcrm-1-0
---

Yay! I've started to understand how to use the [Zolera Soap
Infrastructure](http://pywebsvcs.sourceforge.net/) to communicate with
the SOAP interface of [SugarCRM](http://www.sugarcrm.com). Todays
understatement is hereby delivered: *It's not the easiest thing in the
world*. It doesn't help that most of the methods in the SOAP interface
of [SugarCRM](http://www.sugarcrm.com) are documented like this:

    Documentation:

Well, they do tell which datatypes the expect as well, but not exactly
how they should be filled.

Anyway, today I managed to create a meeting and connect it to the
current user. Yay! Here's the code:

    #!/usr/bin/env python

    from sugarsoap_services import *
    import md5

    import sys

    class LoginError(Exception): pass

    def login(username, password):
        loc = sugarsoapLocator()

        portType = loc.getsugarsoapPortType()

        request = loginRequest()
        uauth = request.new_user_auth()
        request.User_auth = uauth

        uauth.User_name = username
        uauth.Password = md5.new(password).hexdigest()
        uauth.Version = '1.1'

        response = portType.login(request)

        if -1 == response.Return.Id:
            raise LoginError(response.Return.Error)
        return (portType, response.Return.Id)


    def add_meeting(portType, sessionid,
                    date_start, time_start, name, duration_hours):

        gui_req = get_user_idRequest()
        gui_req.Session = sessionid
        user_id = portType.get_user_id(gui_req).Return

        print "user_id", user_id

        se_req = set_entryRequest()
        se_req.Session = sessionid
        se_req.Module_name = 'Meetings'

        se_req.Name_value_list = []
        for (n, v) in [('date_start', date_start),
                       ('time_start', time_start),
                       ('name', name),
                       ('duration_hours', duration_hours),
                       ('assigned_user_id', user_id)]:
            nvl = ns0.name_value_Def('name_value')
            nvl._name = n
            nvl._value = v
            se_req.Name_value_list.append(nvl)

        se_resp = portType.set_entry(se_req)

        meeting_id = se_resp.Return.Id

        # Now let's associate this meeting with the current user, to make
        # it appear in this user's calendar

        sr_req = set_relationshipRequest()
        sr_req.Session = sessionid
        sr_req.Set_relationship_value = sr_req.new_set_relationship_value()
        sr_req.Set_relationship_value.Module1 = 'Meetings'
        sr_req.Set_relationship_value.Module1_id = meeting_id
        sr_req.Set_relationship_value.Module2 = 'Users'
        sr_req.Set_relationship_value.Module2_id = user_id

        sr_resp = portType.set_relationship(sr_req)

        return sr_resp

    if "__main__" == __name__:
        (portType, sessionid) = login('username', 'password')
        response = add_meeting(portType, sessionid, '2006-09-14',
                               '15:00:00', 'Soap Meeting', 1)

Piece of cake, huh? :-)

