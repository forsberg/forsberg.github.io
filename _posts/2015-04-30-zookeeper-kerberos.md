---
layout: post
title: 'Zookeeper + Kerberos Ticket Cache'
tags: [java,kerberos]
redirect_from: /blog/archive/2015/04/30/zookeeper-kerberos
---

Was trying to connect to zookeeper with kerberos authentication. This
was giving me the following "helpful" error message:

    WARN
    [main-SendThread(zookeeper.example.com:2181):ZooKeeperSaslClient$ClientCallbackHandler@459] - 
    Could not login: the client is being asked for a password, but the Zookeeper client code does 
    not currently support obtaining a password from the user. Make sure that the client is 
    configured to use a ticket cache (using the JAAS configuration setting 'useTicketCache=true)' 
    and restart the client. If you still get this message after that, the TGT in the ticket cache 
    has expired and must be manually refreshed. To do so, first determine if you are using a 
    password or a keytab. If the former, run kinit in a Unix shell in the environment of the 
    user who is running this Zookeeper client using the command 'kinit <princ>' 
    (where <princ> is the name of the client's Kerberos principal). If the latter, 
    do 'kinit -k -t <keytab> <princ>' (where <princ> is the name of the Kerberos principal, 
    and <keytab> is the location of the keytab file). After manually refreshing your cache, 
    restart this client. If you continue to see this message after manually refreshing your cache, 
    ensure that your KDC host's clock is in sync with this host's clock.

    [Krb5LoginModule] authentication failed 

I was using the following command line:

    CLIENT_JVMFLAGS="-Djava.security.auth.login.config=/home/forsberg/jaas.conf" zookeeper-client -server zookeeper.example.com:2181

With jaas.conf containing:

    Client {
       com.sun.security.auth.module.Krb5LoginModule required
       useTicketCache=true;
    };

Not a very helpful error message. Adding
**-Dsun.security.krb5.debug=true** to the cmdline gave more
information::
  ~ unsupported key type found the default TGT: 18

This combined with
[https://unix.stackexchange.com/questions/23012/java-could-not-get-the-tgt-from-cache-in-linux-client/23172](https://unix.stackexchange.com/questions/23012/java-could-not-get-the-tgt-from-cache-in-linux-client/23172)
made me realize I had forgotten to install the "Java Cryptography
Extension (JCE) Unlimited Strength Jurisdiction Policy Files" on this
particular machine.

Problem solved.

