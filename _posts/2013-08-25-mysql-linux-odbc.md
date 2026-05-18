---
title: "Configuring ODBC to MySQL from Oracle"
date: 2013-08-25 08:14:00 +0000
last_modified_at: 2013-08-25 08:14:35 +0000
tags:
  - yum
  - ODBC
  - Hetrogenous Services
  - MySQL
  - linux
  - Oracle Developer Day VM
  - unixodbc
---

Sometimes people want to connect to MySQL from Oracle and copy table data between the databases.  You can do that with Oracle Hetrogenous Services via ODBC.  This post will show how to create an odbc connection to your MySQL database which is the first part of this.   
  
For my example, I'm using unixODBC and its on the Oracle public yum repository  

```
[root@localEL5 ~]$ yum install unixODBC
Loaded plugins: security
Setting up Install Process
Resolving Dependencies
> Running transaction check
> Processing Dependency: libboundparam.so.1 for package: unixODBC-devel
> Processing Dependency: libesoobS.so.1 for package: unixODBC-devel
> Processing Dependency: libgtrtst.so.1 for package: unixODBC-devel
> Processing Dependency: libmimerS.so.1 for package: unixODBC-devel
> Processing Dependency: libnn.so.1 for package: unixODBC-devel
> Processing Dependency: libodbc.so.1 for package: unixODBC
.....
> Running transaction check
> Package unixODBC-devel.i386 0:2.2.11-10.el5 set to be updated
> Package unixODBC-libs.i386 0:2.2.11-10.el5 set to be updated
> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package               Arch        Version              Repository         Size
================================================================================
Updating:
 unixODBC              i386        2.2.11-10.el5        el5_latest        290 k
Installing for dependencies:
 unixODBC-libs         i386        2.2.11-10.el5        el5_latest        551 k
Updating for dependencies:
 unixODBC-devel        i386        2.2.11-10.el5        el5_latest        738 k

Transaction Summary
================================================================================
Install       1 Package(s)
Upgrade       2 Package(s)

Total download size: 1.5 M
Is this ok [y/N]: y
Downloading Packages:
(1/3): unixODBC-2.2.11-10.el5.i386.rpm                   | 290 kB     00:02     
(2/3): unixODBC-libs-2.2.11-10.el5.i386.rpm              | 551 kB     00:04     
(3/3): unixODBC-devel-2.2.11-10.el5.i386.rpm             | 738 kB     00:17     
--------------------------------------------------------------------------------
Total                                            60 kB/s | 1.5 MB     00:26     
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing     : unixODBC-libs                                            1/5 
warning: /etc/odbcinst.ini created as /etc/odbcinst.ini.rpmnew
  Updating       : unixODBC                                                 2/5 
  Updating       : unixODBC-devel                                           3/5 
  Cleanup        : unixODBC                                                 4/5 
  Cleanup        : unixODBC-devel                                           5/5 

Dependency Installed:
  unixODBC-libs.i386 0:2.2.11-10.el5                                            

Updated:
  unixODBC.i386 0:2.2.11-10.el5                                                 

Dependency Updated:
  unixODBC-devel.i386 0:2.2.11-10.el5                                           

Complete!
[root@localEL5 ~]$
```

  
Now make sure odbc connector is installed for MySQL. Again, we're using our friend yum to provide it  
  

```
[root@localEL5 ~]$  yum install mysql-connector-odbc
Loaded plugins: security
Setting up Install Process
Resolving Dependencies
There are unfinished transactions remaining. You might consider running yum-complete-transaction first to finish them.
The program yum-complete-transaction is found in the yum-utils package.
> Running transaction check
...
> Finished Dependency Resolution

Dependencies Resolved

=================================================================================================
 Package                      Arch         Version                      Repository          Size
=================================================================================================
Installing:
 mysql-connector-odbc         i386         3.51.26r1127-2.el5           el5_latest         159 k
Installing for dependencies:
 libtool-ltdl                 i386         1.5.22-7.el5_4               el5_latest          37 k

Transaction Summary
=================================================================================================
Install       2 Package(s)
Upgrade       0 Package(s)

Total download size: 196 k
Is this ok [y/N]: y
Downloading Packages:
(1/2): libtool-ltdl-1.5.22-7.el5_4.i386.rpm                               |  37 kB     00:04     
(2/2): mysql-connector-odbc-3.51.26r1127-2.el5.i386.rpm                   | 159 kB     00:01     
-------------------------------------------------------------------------------------------------
Total                                                             21 kB/s | 196 kB     00:09     
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing     : libtool-ltdl                                                              1/2 
  Installing     : mysql-connector-odbc                                                      2/2 

Installed:
  mysql-connector-odbc.i386 0:3.51.26r1127-2.el5                                                 

Dependency Installed:
  libtool-ltdl.i386 0:1.5.22-7.el5_4                                                             

Complete!
[root@localEL5 ~]$
```

  
Now lets  check driver locations and DSNs. Firstly we can check the installed drivers now in the file **/etc/odbcinst.ini**  

```
# driver definitinions
#
#

# Included in the unixODBC package
[PostgreSQL]
Description     = ODBC for PostgreSQL
Driver          = /usr/lib/libodbcpsql.so
Setup           = /usr/lib/libodbcpsqlS.so
FileUsage       = 1

# Driver from the MyODBC package
# Setup from the unixODBC package
[MySQL]
Description     = ODBC for MySQL
Driver          = /usr/lib/libmyodbc.so
Setup           = /usr/lib/libodbcmyS.so
FileUsage       = 1
```

Then, we can specify a DSN to connect with in **/etc/odbc.ini (**Be careful here the option names are case sensitive.  

```
[sakila-connector]
driver=MySQL
Database=sakila
Socket=/var/lib/mysql/mysql.sock
User=root
Password=oracle
```

Finally, we can now check our dsn defined above.  We'll use iSQL from the unixODBC package here.  

```
[oracle@Unknown-08:00:27:c8:2a:1c lib]$ isql -v sakila-connector
+---------------------------------------+
| Connected!                            |
|                                       |
| sql-statement                         |
| help [tablename]                      |
| quit                                  |
|                                       |
+---------------------------------------+
```

Cool. When we get this we are connected via odbc to the DSN.  Now we can prove it by doing a show tables or something to prove its working.   
*NB: If you get an error at this stage asking for libraries, its likely you specified your Drivers incorrectly in the odbcinst.ini.*  
Now we have this working we can setup HS on the Oracle side.
