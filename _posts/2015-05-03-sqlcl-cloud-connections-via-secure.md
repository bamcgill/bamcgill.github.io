---
title: "SQLcl - Cloud connections via Secure Shell tunnels"
date: 2015-05-03 23:39:00 +0000
last_modified_at: 2015-05-03 23:39:34 +0000
tags:
  - cloud
  - sqlcl
  - tunnel
  - SQLDEVELOPER
---

We're always trying to make SQLcl easier to connect to your database, whether its at your place or in the cloud.  So, one other thing we have added to enable you to drill into your cloud databases is an **SSHTUNNEL** command.  Lets take a look at the help for it, which you can get as follows.  
  

```
SQL> help sshtunnel
SSHTUNNEL
---------

Creates a tunnel using standard ssh options 
such as port forwarding like option -L of the given port on the local host 
will be forwarded to the given remote host and port on the remote side. It also supports
identity files, using the ssh -i option
If passwords are required, they will be prompted for.

SSHTUNNEL <username>@<hostname> -i <identity_file> [-L localPort:Remotehost:RemotePort]

Options

-L localPort:Remotehost:Remoteport

Specifies that the given port (localhost) on the local (client) host is to be forwarded to 
the given remote host (Remotehost) and port (Remoteport) on the remote side.  This works by 
allocating a socket to listen to port on the local side.
Whenever a connection is made to this port, the connection is forwarded over 
the secure channel, and a connection is made to remote host & remoteport from 
the remote machine.

-i identity_file
Selects a file from which the identity (private key) for public key authentication is read. 

SQL>
```

  
So for this to work we need to decide which ports locally we are going to use and which remote machine and port we want to use to map our ports from local to remote.  We also need a RSA file from the target host.  In this example, we have created one with the default name of **id\_rsa.**  

The format of the flags follow the standard ssh rules and options, so -i for identity files and -L for port forwarding.  Heres an example connecting to a remote host via a tunnel.  
  

```
(bamcgill@daedalus.local)–(0|ttys000|-bash)–(Mon May 04|12:16:46)
(~/.ssh) $sql /nolog

SQLcl: Release 4.1.0 Release Candidate on Mon May 04 00:16:58 2015

Copyright (c) 1982, 2015, Oracle.  All rights reserved.

SQL> sshtunnel bamcgill@gbr30060.uk.oracle.com -i ./id_rsa -L 8888:gbr30060.uk.oracle.com:1521

Password for bamcgill@gbr30060.uk.oracle.com ********
ssh tunnel connected

SQL> connect barry/oracle@localhost:8888/DB11GR24
Connected

SQL> select 'test me' as BLRK from dual weirdtable

BLRK  
-------
test me

SQL>
```

  
You can download SQLcl from OTN [here](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/sqldev-41ea-2372780.html) and give this a try when the next EA is released.
