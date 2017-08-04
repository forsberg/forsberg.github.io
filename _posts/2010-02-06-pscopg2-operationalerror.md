---
layout: post
title: 'PostgreSQL/Python/psycopg2: Confusing error, port setting required for socket connections'
tags: [django,python]
redirect_from: /blog/archive/2010/02/06/pscopg2-operationalerror
---

When trying to get my local development copy of this website running
after upgrading my Ubuntu, I got the following confusing error message
from the psycopg2 python module:

    psycopg2.OperationalError: could not connect to server: No such file or directory
            Is the server running locally and accepting
        connections on Unix domain socket  "/var/run/postgresql/.s.PGSQL.5432"?

My django settings file was correct:

    DATABASE_ENGINE = 'postgresql_psycopg2'  # 'postgresql_psycopg2', 'postgresql', 'mysql', 'sqlite3' or 'oracle'.
    DATABASE_NAME = 'dbname'                 # Or path to database file if using sqlite3.
    DATABASE_USER = 'dbuser'                 # Not used with sqlite3.
    DATABASE_PASSWORD = 'dbpassword'         # Not used with sqlite3.
    DATABASE_HOST = ''                       # Set to empty string for localhost. Not used with sqlite3.
    DATABASE_PORT = ''                       # Set to empty string for default. Not used with sqlite3.

Confusing, since my Postgres server was running and I could connect
using psql:

    psql -U dbuser -W dbname

This turned out to be one of these problems when Google is of no help -
others had the same problem, but I could only find posts where people
asked the question, no posts where the actual solution was found.

The cause of the problem was that my PostgreSQL installation was
configured to listen on port 5433 instead of the default 5432, and as
seen in the error message, the port number is part of the path to the
unix socket. The different port was probably setup when I upgraded my
Ubuntu, since that installed PostgreSQL 8.4 without completely removing
PostgreSQL 8.3. The latter is configured to listen on the default port.

The solution is to either configure the running PostgreSQL to listen on
port 5432 by modifying `/etc/postgresql/8.4/main/postgresql.conf`, or by
modifying the Django configuration by setting the port:

::

> DATABASE\_PORT = '5433'

