---
title: "Configuring Heterogeneous Services for Oracle and MySQL"
date: 2013-08-25
---

This is the second part of a post which @aejes (John Scott) proposed on Friday to do some copying of tables using heterogeneous services. And, as usual, I'm using this to detail how to do this, for you and for me.  
From last post on configuring ODBC on Linux. we have the MySQL side set up and ready to go. If you have not tested that yet, you'll need to get over there and try it first before coming here.  (It saves a whole load of heart ache figuring out why it doesn't work.)  
  
Configure your listener.  Mine is in the default **$ORACLE\_HOME/network/admin**.  This entry, I've added to my listener, you should be able to find in your own **$ORACLE\_HOME/hs/admin/listener.ora.sample**. I've copied this verbatim from there.  On install, the file is modified with all your defaults like your $ORACLE\_HOME.  
  

```
SID_LIST_LISTENER=
  (SID_LIST=
      (SID_DESC=
         (SID_NAME=dg4odbc)
         (ORACLE_HOME=/home/oracle/app/oracle/product/11.2.0/dbhome_2)
         (PROGRAM=dg4odbc)
      )
  )
```

Now, we fire it up and see if its listening for a connection from ODBC.  

```
[oracle@devdayEL5 admin]lsnrctl start

LSNRCTL for Linux: Version 11.2.0.2.0 - Production on 25-AUG-2013 04:38:30

Copyright (c) 1991, 2010, Oracle.  All rights reserved.

Starting /home/oracle/app/oracle/product/11.2.0/dbhome_2/bin/tnslsnr: please wait...

TNSLSNR for Linux: Version 11.2.0.2.0 - Production
System parameter file is /home/oracle/app/oracle/product/11.2.0/dbhome_2/network/admin/listener.ora
Log messages written to /home/oracle/app/oracle/diag/tnslsnr/Unknown-08:00:27:c8:2a:1c/listener/alert/log.xml
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=80))(PROTOCOL_STACK=(PRESENTATION=HTTP)(SESSION=RAW)))
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=21))(PROTOCOL_STACK=(PRESENTATION=FTP)(SESSION=RAW)))

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=0.0.0.0)(PORT=1521)))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 11.2.0.2.0 - Production
Start Date                25-AUG-2013 04:38:30
Uptime                    0 days 0 hr. 0 min. 0 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Parameter File   /home/oracle/app/oracle/product/11.2.0/dbhome_2/network/admin/listener.ora
Listener Log File         /home/oracle/app/oracle/diag/tnslsnr/Unknown-08:00:27:c8:2a:1c/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=80))(PROTOCOL_STACK=(PRESENTATION=HTTP)(SESSION=RAW)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=21))(PROTOCOL_STACK=(PRESENTATION=FTP)(SESSION=RAW)))
Services Summary...
Service "dg4odbc" has 1 instance(s).
  Instance "dg4odbc", status UNKNOWN, has 1 handler(s) for this service...
The command completed successfully
[oracle@devdayEL5 admin]
```

And we can see that it is listening. Cool.  Now. Back to figuring out our ODBC.  We need to configure our agent, which you'll have seen already above in the listener.ora addtion we made.  Its dg4odbc, a pseudo acronym I'm sure you can work out.  We need to go back the the $ORACLE\_HOME/hs/admin directory and work on the gateway configuration file.  Here's the way it looks like by default.  

```
[oracle@devdayEL5 admin]cat initdg4odbc.ora 
# This is a sample agent init file that contains the HS parameters that are
# needed for the Database Gateway for ODBC

#
# HS init parameters
#
HS_FDS_CONNECT_INFO = 
HS_FDS_TRACE_LEVEL = 
HS_FDS_SHAREABLE_NAME = 

#
# ODBC specific environment variables
#
set ODBCINI=


#
# Environment variables required for the non-Oracle system
#
set =
```

We need to make some changes to it to make it work for our MySQL database that we configured.  Here's what you need to change to get it working.  

```
#
# HS init parameters
#
HS_FDS_CONNECT_INFO = sakila-connector
HS_FDS_TRACE_LEVEL = 4 
```

```
#0 or false to turn this off
HS_FDS_SHAREABLE_NAME = /usr/lib/libodbc.so 
```

```
#lib from unixodbc not mysql driver

#
# ODBC specific environment variables
#
set ODBCINI=/etc/odbc.ini #location of the DSN for HS
```

That's all our listener and gateway configuration done.  Lastly we need to test that we can connect.  REmember from last time, we used iSQL from unixODBC to test our DSN. We can make sure that works before we test on the oracle side using TNS. Which reminds me, we also need to add a TNS entry for us to us. Lets do that now.  In the **$ORACLE\_HOME/hs/admin** directory, there is a tnsnames.ora.sample file which you can use to add to your tnsnames.ora in $ORACLE\_HOME/network/admin.  

```
dg4odbc  =
  (DESCRIPTION=
    (ADDRESS=(PROTOCOL=tcp)(HOST=localhost)(PORT=1521))
    (CONNECT_DATA=(SID=dg4odbc))
    (HS=OK)
  )
```

The only thing I changed here is to rename dg4odbc in this entry to sakila which matches the demo mysql database I'm trying to do something with.  Now, the moment of truth.  We can use tnsping to test our connection.  

```
[oracle@devdayEL5 admin]tnsping sakila

TNS Ping Utility for Linux: Version 11.2.0.2.0 - Production on 25-AUG-2013 05:13:14

Copyright (c) 1997, 2010, Oracle.  All rights reserved.

Used parameter files:


Used TNSNAMES adapter to resolve the alias
Attempting to contact (DESCRIPTION= (ADDRESS=(PROTOCOL=tcp)(HOST=localhost)(PORT=1521)) (CONNECT_DATA=(SID=dg4odbc)) (HS=OK))
OK (10 msec)
```

Magic.  Lastly, we can create a database link in Oracle to connect to mysql and get some data out of it. We connect to our database and do this.  

```
SQL> create public database link mysql
  2  connect to "root" 
  3  identified by "oracle"
  4  using 'dg4odbc'
  5  ;
SQL> /

Database link created.

SQL>
```
