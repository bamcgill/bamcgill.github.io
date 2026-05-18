---
title: "Remote Debugging with SQL Developer revisited."
date: 2012-04-12 21:41:00 +0000
last_modified_at: 2012-04-12 21:41:27 +0000
tags:
  - remote debug
  - dbms_output
  - oracle
  - sqlplus
  - SQLDEVELOPER
---

As part of the development process, we all have to work out the bugs in our code.  For all of us who use SQLDeveloper , we know how to debug with SQL Developer. Compile for Debug, breakpoint and go.  However, People still get confused by what remote debugging is and how it works.  At its most basic, it allows us to run a procedure in a session and debug if from another.  
  
So, Lets say we have a simple procedure on employees table like this.
  
  

```
create or replace
FUNCTION GET_EMP_NAME 
(
  ID IN NUMBER  
) RETURN VARCHAR2 AS 
name varchar2(100);
BEGIN
 select first_name||' '||last_name into name from employees
 where employee_id = ID;
  RETURN name;
END GET_EMP_NAME;
```

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjbVQq8J2-ltu21OsyK4UciIKvrWG7siCZ516fKzvRM-1ZIUvcaB8U27DwYOEpIit36fF3zkPWxmEG-KnSKAtWRzSD_aY7h-eqd2Whss0SzZilyvnS01JQZgC7btBjdKiFt1elMkkCA8AI/s1600/Screen+Shot+2012-04-12+at+17.54.49.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjbVQq8J2-ltu21OsyK4UciIKvrWG7siCZ516fKzvRM-1ZIUvcaB8U27DwYOEpIit36fF3zkPWxmEG-KnSKAtWRzSD_aY7h-eqd2Whss0SzZilyvnS01JQZgC7btBjdKiFt1elMkkCA8AI/s1600/Screen+Shot+2012-04-12+at+17.54.49.png)

  
  
We can compile this for debug in SQLDeveloper as normal.  Now, for remote debugging, we want to go to another session and run this function there.  For clarity, we can do it in SQL\*Plus.  Before that however, we need to switch on the remote debugger listener so we can attach to a session.  So, firstly, right click on your connection and choose remote debug, which will pop up a little window  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgrC1ZfQdOlHt8OQ5z1xJZ-cL8Olmy66YKHwz59JFwY1iBAdf5BXycDLoFmgFAU02Y2TBJWDGXpqN9AuUHUExCqqXhh2TQTg2ahSK4lA15YZgadBnyTWMnj50aNaQ5q2G_bpaKh7g3NUlc/s1600/Screen+Shot+2012-04-12+at+20.21.19.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgrC1ZfQdOlHt8OQ5z1xJZ-cL8Olmy66YKHwz59JFwY1iBAdf5BXycDLoFmgFAU02Y2TBJWDGXpqN9AuUHUExCqqXhh2TQTg2ahSK4lA15YZgadBnyTWMnj50aNaQ5q2G_bpaKh7g3NUlc/s1600/Screen+Shot+2012-04-12+at+20.21.19.png)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs2RkAVR4A8p34-R2HvKbfETG0wpg-_oRkaScDo-CXbggZSHi8UkMou6nOe1X-HxgdBlCMY1EI9ibXSitLK3e1yjA9is6Q5_pexxpRV3FxrZpGHg_CR2_2UTxheir7v55hzsZF5LCfLIU/s320/Screen+Shot+2012-04-12+at+20.16.01.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs2RkAVR4A8p34-R2HvKbfETG0wpg-_oRkaScDo-CXbggZSHi8UkMou6nOe1X-HxgdBlCMY1EI9ibXSitLK3e1yjA9is6Q5_pexxpRV3FxrZpGHg_CR2_2UTxheir7v55hzsZF5LCfLIU/s1600/Screen+Shot+2012-04-12+at+20.16.01.png)  

For our purposes, on localhost, we dont need to add any other information, but if you are connecting to another database on another machine, add the host name to the local address field and choose an appropriate port.  When you click ok on this, the Run manager is shown with the listener details on there as shown above.

Now, here we are with SQL\*Plus, fire it up with our demo user and make sure to execute the command

execute DBMS\_DEBUG\_JDWP.CONNECT\_TCP('127.0.0.1',4000);

and then we can run our function as described above.

```
[oracle@localhost ~]$ sqlplus hrdemo/hrdemo

SQL*Plus: Release 11.2.0.2.0 Production on Thu Apr 12 19:16:37 2012

Copyright (c) 1982, 2010, Oracle.  All rights reserved.

Connected to:
Oracle Database 11g Enterprise Edition Release 11.2.0.2.0 - Production
With the Partitioning, OLAP, Data Mining and Real Application Testing options

HRDEMO@ORCL> set serveroutput on
HRDEMO@ORCL> execute DBMS_DEBUG_JDWP.CONNECT_TCP('127.0.0.1',4000);

PL/SQL procedure successfully completed.

HRDEMO@ORCL> begin
  2  dbms_output.put_line(get_emp_name(100));
  3  end;
  4  /
```

  
Once we run the anonymous bock, the remote debugger kicks in and we stop at the appropriate breakpoint in the code.   
  
On a last note, this works well in Application Express too so when you make a call to a function which you have remote debug switched on for, the debugger will break on the line as long as you have debug switched on in the developer toolbar.
