---
title: "Developer Days VM Startup and Shutdown, SQLcl"
date: 2016-06-16 12:19:00 +0000
last_modified_at: 2016-06-16 12:19:01 +0000
tags:
  - headless
  - oracle
  - virtualbox
  - SQLDEVELOPER
  - linux
  - MACOS
  - sqlcl
  - sqlplus
---

If you're developing on a remote platform, chances are that you are using a Virtual Machine. (VM)  In Oracle, we release a virtual machine called the  "[Oracle Developer Days](http://www.oracle.com/technetwork/database/enterprise-edition/databaseappdev-vm-161299.html)".    This is available on the [Oracle Technology Network](http://www.oracle.com/technetwork/index.html) and ala [google](http://bfy.tw/6IUN).  Todays hack is setting up headless vm's, ports and aliases to speed up your day. (This post took a lot longer to write that the aliases we set up!)  
  
For this virtual machine on [Virtual Box](https://www.virtualbox.org/), we have a bunch of cool stuff to get your teeth into, prebuilt and configured, ready to go.  Most of the time, we all start our VM from the virtual box front end like this from the application and use the guy front end into the VM.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirZE4s3o4G8-NPhPeAwM0X6vOZ-Pr3o0PcfOG7U9Yl5BJoAmBDHJafs999KliSvmZmke1OPbyXdlbQLbtSBov2yDfTD2Rd2H99dQhEi_2qFUGH9AhuGuxLfLBvTNUbBUVoRz6Ss2cwOwc/s320/Screen+Shot+2016-06-16+at+12.06.24.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirZE4s3o4G8-NPhPeAwM0X6vOZ-Pr3o0PcfOG7U9Yl5BJoAmBDHJafs999KliSvmZmke1OPbyXdlbQLbtSBov2yDfTD2Rd2H99dQhEi_2qFUGH9AhuGuxLfLBvTNUbBUVoRz6Ss2cwOwc/s1600/Screen+Shot+2016-06-16+at+12.06.24.png)

  
You can click on the network tab and click port forwarding to see how you are allowing access to this virtual machine.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi85NiY6zBuWEIAAw9dPdbBeTOLcf7K8Af5DXpMVlmqb5hQhkcpjdfHykISQt4rVXjaKLTSU2puSgeWeap7mFYuV_Nlp7mc16IBiHNchciaMOT2Q-ZyXeAJWH_GUzNvWWE1XEypGyrfAM4/s320/Screen+Shot+2016-06-16+at+12.13.24.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi85NiY6zBuWEIAAw9dPdbBeTOLcf7K8Af5DXpMVlmqb5hQhkcpjdfHykISQt4rVXjaKLTSU2puSgeWeap7mFYuV_Nlp7mc16IBiHNchciaMOT2Q-ZyXeAJWH_GUzNvWWE1XEypGyrfAM4/s1600/Screen+Shot+2016-06-16+at+12.13.24.png)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvQKJYIgOdmkRLSuXSiJlS5bPEqxQ1si8gkxNYTJQm8wEWDk7kf6Ofr8ASjegHcNUm9vdt36QwO1YSybx-Xu2nFBeBAzBRXrBCJg0VCny7g11bU6vfkHH7dCNemg2BiCrveZsArLjDCWA/s320/Screen+Shot+2016-06-16+at+12.13.34.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvQKJYIgOdmkRLSuXSiJlS5bPEqxQ1si8gkxNYTJQm8wEWDk7kf6Ofr8ASjegHcNUm9vdt36QwO1YSybx-Xu2nFBeBAzBRXrBCJg0VCny7g11bU6vfkHH7dCNemg2BiCrveZsArLjDCWA/s1600/Screen+Shot+2016-06-16+at+12.13.34.png)

Clicking on your VM in the user interface, you can start it up and get the full GUI to work from.

|  |
| --- |
|  |
| Normal VM startup within the GUI |

This takes a while and has to be done every time you are starting up which is too many times.  Like any engineer, we are all trying to reduce the number of times we have to do the same thing so I like to make these into command line calls and make the GUI disappear so we can ssh into the virtual machine.

From above, we can see that ssh is mapped to port 2222 on the host for this guest virtual machine so there should be no issues in working this way.   To startup your VM from the command line like above, run this below (obviously changing the name of your VM before you do!)  This will open a window and startup your VM.

vboxmanage startvm "Oracle DB Developer VM" --type=gui

You can also start up your virtual machine in a headless session, you can run this command, very similar to the one above to do that.

(bamcgill@daedalus)–(0|ttys001|-bash)

(~) $vboxmanage startvm "Oracle DB Developer VM" --type headless

Waiting for VM "Oracle DB Developer VM" to power on...

VM "Oracle DB Developer VM" has been successfully started.

(bamcgill@ daedalus)–(0|ttys001|-bash)

(~) $

and thats it. the machine will boot, start the database and start the listeners.  you can then ssh into your machine like this.

(bamcgill@ daedalus)–(0|ttys001|-bash)

(~) $ssh -p 2222 oracle@localhost

oracle@localhost's password:

Last login: Thu Jun 16 07:35:21 2016

[oracle@vbgeneric ~]$ sqlplus barry/oracle

SQL\*Plus: Release 12.1.0.2.0 Production on Thu Jun 16 07:38:20 2016

Copyright (c) 1982, 2014, Oracle.  All rights reserved.

Last Successful login time: Thu Jun 16 2016 06:30:17 -04:00

Connected to:

Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production

With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL> Disconnected from Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production

With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

[oracle@vbgeneric ~]$ logout

Connection to localhost closed.

(bamcgill@daedalus)–(0|ttys001|-bash)

(~) $

All very cool and means I can have aliases setup to do this too so I don't have to remember all the long bits of a vboxmanage statement!

(bamcgill@daedalus)–(0|ttys001|-bash)

(~) $alias | grep vbox

alias headless='vboxmanage startvm "Oracle DB Developer VM" --type headless'

alias poweroff='vboxmanage controlvm "Oracle DB Developer VM" poweroff'

alias startvm='vboxmanage startvm "Oracle DB Developer VM" --type=gui'

alias vboxsave='vboxmanage controlvm "Oracle DB Developer VM" savestate'

(bamcgill@daedalus)–(0|ttys001|-bash)

(~) $

**poweroff**  rips the rug from under the VM and it is reset

**savestate** saves the VM like a most recent snapshot and when started again, the VM is refreshed with this state.

When all this is setup, you can connect with [SQLcl](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html).  By default, sqlcl will look at a few connect strings when you connect, so you can try sql user/password in your host machine.

(bamcgill@ daedalus)–(0|ttys001|-bash)

(~) $sql barry/oracle

SQLcl: Release 4.2.0.16.167.1601 RC on Thu Jun 16 13:01:44 2016

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Last Successful login time: Thu Jun 16 2016 13:01:44 +01:00

Connected to:

Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production

With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

BARRY@orcl🍻🍺 >

Fantastic.  Look out for more great features on [Oracle SQLcl and SQLDeveloper](http://www.oracle.com/technetwork/developer-tools/sql-developer/overview)with [Kris](http://krisrice.blogspot.com/), [Jeff](http://www.thatjeffsmith.com/) , [Dermot](http://dermotoneill.blogspot.co.uk/) and  [Turloch](http://totierne.blogspot.co.uk/)

SaveSave
