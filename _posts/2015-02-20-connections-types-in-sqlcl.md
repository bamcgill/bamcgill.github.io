---
title: "Connections Types  in SQLcl"
date: 2015-02-20 11:07:00 +0000
last_modified_at: 2015-02-20 11:07:22 +0000
tags:
  - Connections
  - oracle
  - SQLDEVELOPER
  - glogin
  - Oracle Developer Day VM
  - sqlplus
  - sqlcl
---

We support many ways to connect in SQLcl, including lots from SQL\*Plus which we need to support to make sure all your SQL\*Plus scripts work exactly the same way using SQLcl as with SQL\*Plus.

I've added several ways to show how to connect to SQLcl.  If there is one you want to see added that is not here, let me know and I'll add it to the list.  So far, We have below:

- EZConnect
- TWO\_TASK
- TNS\_ADMIN
- LDAP

At any time when connected you can use the command '**SHOW JDBC**'  to display what the connection is and how we are connected.  Here's some details of the types above.  

**EZCONNECT**

The easy connect naming method eliminates the need for service name lookup in the tnsnames.ora files for TCP/IP environments.  It extends the functionality of the host naming method by enabling clients to connect to a database server with an optional port and service name in addition to the host name of the database:

```
 $sql barry/oracle@localhost:1521/orcl  
 SQLcl: Release 4.1.0 Beta on Fri Feb 20 10:15:12 2015  
 Copyright (c) 1982, 2015, Oracle. All rights reserved.  
 Connected to:  
 Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production   
 SQL>
```

**TWO\_TASK**

The TWO\_TASK (on UNIX) or LOCAL (on Windows) environment variable can be set to a connection identifier. This removes the need to explicitly enter the connection identifier whenever a connection  is made in SQL\*Plus or SQL\*Plus Instant Client.

In SQLcl, we can set this up as a jdbc style connection like this

  
  

```
$export TWO_TASK=localhost:1521/orcl
```

  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUJd0IIRR-bIorD3ttFuHbsv9X5ZNIASDvP-vJmTQqnAafQh1seUbLigEDi0uumdoedaEFvoAjP0BU2CHWUTEXHAy2bkMY3a9YK2lJd4JFoWBhcgrcddT0c3M86Xm2lbLVd-iCRbNxF6g/s1600/bamcgill_%E2%80%94_java_%E2%80%94_bash_%E2%80%94_Novel_%E2%80%94_ttys000_%E2%80%94_102%C3%9733_%E2%80%94_%E2%8C%981_and_Java_-_Eclipse_-__Users_bamcgill_code_workspace.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUJd0IIRR-bIorD3ttFuHbsv9X5ZNIASDvP-vJmTQqnAafQh1seUbLigEDi0uumdoedaEFvoAjP0BU2CHWUTEXHAy2bkMY3a9YK2lJd4JFoWBhcgrcddT0c3M86Xm2lbLVd-iCRbNxF6g/s1600/bamcgill_%E2%80%94_java_%E2%80%94_bash_%E2%80%94_Novel_%E2%80%94_ttys000_%E2%80%94_102%C3%9733_%E2%80%94_%E2%8C%981_and_Java_-_Eclipse_-__Users_bamcgill_code_workspace.jpg)

  
**TNS\_ADMIN**  
  
  
Local Naming resolves a net service name stored in a tnsnames.ora file stored on a client.  We can set the location of that in the **TNS\_ADMIN** variable.  
  

```
 $export TNS_ADMIN=~/admin
```

  
An example tons entry is shown here below.  
  

```
 $cat tnsnames.ora   
 BLOG =  
 (DESCRIPTION =  
 (ADDRESS=(PROTOCOL=tcp)(HOST=localhost)(PORT=1521) )  
 (CONNECT_DATA=  
 (SERVICE_NAME=orcl) ) )
```

  
we can then use the entry to connect to the database.  
  

```
 $sql barry/oracle@BLOG  
 SQLcl: Release 4.1.0 Beta on Fri Feb 20 10:29:14 2015  
 Copyright (c) 1982, 2015, Oracle. All rights reserved.  
 Connected to:  
 Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production   
 SQL>
```

  
**LDAP**  
  
We've already written about LDAP connections [here](http://barrymcgillin.blogspot.co.uk/2015/01/sqlcl-ldap-anyone.html).  Here's a quick review.  
  

```
  set LDAPCON jdbc:oracle:thin:@ldap://scl58261.us.oracle.com:389/#ENTRY#,cn=OracleContext,dc=ldapcdc,dc=lcom
```

  
  

```
 $export LDAPCON=jdbc:oracle:thin:@ldap://scl58261.us.oracle.com:389/#ENTRY#,cn=OracleContext,dc=ldapcdc,dc=lcom   
 $sql /nolog  
 SQLcl: Release 4.1.0 Beta on Fri Feb 20 10:37:02 2015  
 Copyright (c) 1982, 2015, Oracle. All rights reserved.  
 SQL> connect barry/oracle@orclservice_test(Emily's Desktop)   
 Connected  
 SQL>
```

  
If we have more types to add, then they will appear here.  Let us know what you want to see.
