---
title: "Using History Keys in SQL*Plus"
date: 2012-07-19 18:57:00 +0000
last_modified_at: 2012-07-19 18:58:56 +0000
tags:
  - virtualbox
  - SQL*Plus
  - command line
  - Oracle Developer Day VM
  - utilities
  - SQL Developer
---

I was working through a bug the other day and using SQL\*Plus, which for the most part doesn't annoy me too much.  However, one of the things that does, is having to retype lots of stuff. (We dont have that problem in [SQL Developer](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html)).

  
Having hunted around for a few minutes, I found rlwrap which is a GNU readline wrapper.  All this means is that when we use it on SQL\*Plus, it give us keyboard history and user defined completion.  I've found a few posts about it too, which are referred to below, but I wanted to do this for our virtual machine.  
  
We use our [Oracle Developer Days VM](http://www.oracle.com/technetwork/community/developer-vm/index.html) a lot internally as its great for spooling a DB having a full environment ready to play with and test features.  I'm using that for this post.  
  
You can download rlwrap from [here](http://utopia.knoware.nl/~hlub/uck/rlwrap/).  There are also RPMs available too.  I pulled down the tar ball.   Expand it out and you have a bunch of files for a standard build  
  
Firstly, we need to run the ./configure script to find all the dependencies.  You can see a cut down version of the output of that below.  
  
  

```
checking for tgetent in -lcurses... no
checking for tgetent in -lncurses... no
checking for tgetent in -ltermcap... no
configure: WARNING: No termcap nor curses library found
checking for readline in -lreadline... no
configure: error: 

You need the GNU readline library(ftp://ftp.gnu.org/gnu/readline/ ) to build
this program!

[root@localhost rlwrap-0.37]#
```

  
Running configure on my system flagged that I didnt have the readline package installed.   However, when I went to install it with  
  

```
[root@localhost ~]# yum install readline
Loaded plugins: security
Setting up Install Process
Package readline-5.1-3.el5.i386 already installed and latest version
Nothing to do
```

  
I discovered it was already installed.  A quick look through the config.log tho, from the configure process shows that the -lreadline library dependency could not be satisfied.  It needed the development package to build.  
  

```
[root@localhost rlwrap-0.37]# yum install readline-devel
```

  

```
Total download size: 202 k
Is this ok [y/N]: y
Downloading Packages:
(1/2): libtermcap-devel-2.0.8-46.1.i386.rpm              |  56 kB     00:00     
(2/2): readline-devel-5.1-3.el5.i386.rpm                 | 146 kB     00:01     
--------------------------------------------------------------------------------
Total                                            85 kB/s | 202 kB     00:02     
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing     : libtermcap-devel                                         1/2 
  Installing     : readline-devel                                           2/2 

Installed:
  readline-devel.i386 0:5.1-3.el5                                               

Dependency Installed:
  libtermcap-devel.i386 0:2.0.8-46.1                                            

Complete!
[root@localhost rlwrap-0.37]#
```

  
Ok, Now to try configure again..  
  

```
configure: creating ./config.status
config.status: creating Makefile
config.status: creating filters/Makefile
config.status: creating doc/Makefile
config.status: creating src/Makefile
config.status: creating doc/rlwrap.man
config.status: creating config.h
config.status: executing depfiles commands

Now do:
    make (or gmake)  to build rlwrap
    make check       for instructions how to test it
    make install     to install it

[root@localhost rlwrap-0.37]#
```

  
Running the configure again, succeeded creating my makefile. Great.  Now run the following to build it and install it in the right place and we should be getting places.  
  

```
[root@localhost rlwrap-0.37]# make
```

and
  

```
[root@localhost rlwrap-0.37]# make install
```

  
Great. Now, rlwrap is installed in /usr/local/bin and we can use it in our oracle terminal window.   
  

```
[oracle@localhost rlwrap-0.37]$ rlwrap
Usage: rlwrap [options] command ...

Options:
  -a[password:]              --always-readline[=password:]
  -A                         --ansi-colour-aware
  -b  <chars>                --break-chars=<chars>
```

  
Now we can use rlwrap to run SQL\*Plus, which gets me back to what I wanted to do at the start.  I've kicked this off with the '-c' option.  
  

```
[oracle@localhost ~]$ rlwrap -c sqlplus barry/barry

SQL*Plus: Release 11.2.0.2.0 Production on Thu Jul 19 17:51:51 2012

Copyright (c) 1982, 2010, Oracle.  All rights reserved.

Connected to:
Oracle Database 11g Enterprise Edition Release 11.2.0.2.0 - Production
With the Partitioning, OLAP, Data Mining and Real Application Testing options

BARRY@ORCL>
```

  
Now my up and down arrows work AND with the '-c' option for rlwrap, we get filename completion for free.  
  

```
BARRY@ORCL> @re
remote.sql          reset_imdbcache     reset_xmldb
repos/              reset_sqldev        reset_xmldb~
reset_OE.sql        reset_svn           
reset_apex          reset_xdbPorts.sql  
BARRY@ORCL> @re
```

  
So, now I'm a lot happier and can zip through loading files and getting my previous statements.  
  
Now, I know there are issues with using this when we redirect files into SQL\*Plus, on other blogs like [this](http://sysdba.wordpress.com/2006/10/08/how-to-use-rlwrap-to-get-a-command-history-in-sqlplus/) from Lutz Hartmann, but for me and working with plus in a terminal window, this will do nicely.
