---
title: "login.sql, SQLPROMPT and worksheets"
date: 2011-11-19 01:57:00 +0000
last_modified_at: 2011-11-22 11:52:00 +0000
tags:
  - glogin
  - sqlpath
  - SQL*Plus
  - SQLDEVELOPER
---

SQLDeveloper has had support for a login.sql for several releases now.  You can set this in the preferences at  
  

```
Tools -> Prefernces -> Database
```

  
You can set your login.sql here.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXAUP2cAnIwpz0Sqc8hWTsUzhqQPd9AagN6vEZ-_d73CWcsxClvnXqT9V4AHg7IpfYhvNTzfLTSi2kGW8K-vff8HKciLe_18qQE_cPDwP85HPtqoWs_td6QhvoTwKlCJKlSjv4Lvj1Zg4/s400/loginpref.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXAUP2cAnIwpz0Sqc8hWTsUzhqQPd9AagN6vEZ-_d73CWcsxClvnXqT9V4AHg7IpfYhvNTzfLTSi2kGW8K-vff8HKciLe_18qQE_cPDwP85HPtqoWs_td6QhvoTwKlCJKlSjv4Lvj1Zg4/s1600/loginpref.PNG)

  
Now, when SQL\*Plus starts up, it looks for a global login script called glogin.sql in the $ORACLE\_HOME/sqlplus/admin directory. If found, this script will be executed.  
Thereafter, SQL\*Plus will try to find a local login script called login.sql in the directory where you start sqlplus from, alternatively the directories listed in the SQLPATH environment variable. When found, sqlplus will execute it.  Here's my login.sql for SQL\*Plus  

```
define gname=idle
column global_name new_value gname
select lower(user) || '@' || substr( global_name, 1, decode( dot, 0, length(global_name), dot-1) ) global_name
  from (select global_name, instr(global_name,'.') dot from global_name );
set sqlprompt '&gname> '
```

  
and when I login to sqlplus, I get this.  

```
SQL*Plus: Release 11.2.0.2.0 Beta on Mon Nov 21 11:05:58 2011

Copyright (c) 1982, 2010, Oracle.  All rights reserved.

Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - Beta

GLOBAL_NAME
-----------------------------------------------------------------

barry@XE

barry@XE>
```

  
Obviously, in SQLDeveloper, this won't mean anything as prompts are not there, however, the variables you set and the column formats, titles, pagesizes etc, will be preserved.  
  
For example, in our login2.sql  list in the preferences above, we set a couple of column settings and for fun, lets set the prompt variable too.   
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg2ZQ417BPumuocuZ6FuJ-0VYK5hscBXLiaILu_Cu4Wq0GC26KCUEXlWFPFWLXbBrTUpc1A1DVxUXSXJiilhy1wNCpAdI8GfsLQJdtPUbZ992Lv3B3At_SMeUvilc4VWA-i3qPXMtJyaAI/s400/login2sql.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg2ZQ417BPumuocuZ6FuJ-0VYK5hscBXLiaILu_Cu4Wq0GC26KCUEXlWFPFWLXbBrTUpc1A1DVxUXSXJiilhy1wNCpAdI8GfsLQJdtPUbZ992Lv3B3At_SMeUvilc4VWA-i3qPXMtJyaAI/s1600/login2sql.PNG)

  
As shown above, we now have a login.sql defined in the preferences. When we make a connection, the login.sql will be run and any settings will be applied to the database.  We will also hold onto any SQL\*Plus variables defined so they can be used in any worksheet that is started using this connection.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgWjjqSAWpSujsnv1Hkg9H-to3gkyDpyvRGhp3oGINJcBUKdZ7qC9PkZnVkEtC_nvMMWxqNp78Sekt3I-bKvLhxSSHgUwes_8Fak-2pullu0q5DSbeEi66PvQIwK8kafRvIv4rsZiOlIv8/s1600/connectbarry.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgWjjqSAWpSujsnv1Hkg9H-to3gkyDpyvRGhp3oGINJcBUKdZ7qC9PkZnVkEtC_nvMMWxqNp78Sekt3I-bKvLhxSSHgUwes_8Fak-2pullu0q5DSbeEi66PvQIwK8kafRvIv4rsZiOlIv8/s1600/connectbarry.PNG)

When you connect, you get the new worksheet, and the sql that was run produces any output in the messages.log.  The reason for this is you can connect to the database without spawning a worksheet and this lets you know of any output from that login script we put together earlier.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgnM6iiExivCRkTJKjq6HWljnaCoqXtscEKpdgvTWNqDvpdMeHDXsUX8e5K3mFu9sXJW3cOUG5IL6jZAGcEx1h2PYGveGRNhjGlXPAv2WWS16PkpOVIzwFq33g-YW7kNk51bdW5jL2jvRg/s1600/loginsqloutput.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgnM6iiExivCRkTJKjq6HWljnaCoqXtscEKpdgvTWNqDvpdMeHDXsUX8e5K3mFu9sXJW3cOUG5IL6jZAGcEx1h2PYGveGRNhjGlXPAv2WWS16PkpOVIzwFq33g-YW7kNk51bdW5jL2jvRg/s1600/loginsqloutput.PNG)

  
Now, we are connected, any worksheet created on that connection will have the context of the original script.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh9ea5d09QGkd0C-pTWndz1O94hl3xKkKf4BjaFgcW9VCImNSzgfWt5Z_znd16S21Ww5UBudMgy1f3sEsJ1T_N2jouJBZGdp118wkl1yX5juNDdJe73nTOOqLJphfiHrlS_JcDIq3n78hU/s320/logindefine.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh9ea5d09QGkd0C-pTWndz1O94hl3xKkKf4BjaFgcW9VCImNSzgfWt5Z_znd16S21Ww5UBudMgy1f3sEsJ1T_N2jouJBZGdp118wkl1yX5juNDdJe73nTOOqLJphfiHrlS_JcDIq3n78hU/s1600/logindefine.PNG)

  
  
Lastly, you can also set your worksheet name to be a substitution variable as well  
  
  

```
set worksheetname &gname
```

  
which will swap you default worksheet name to your connection credentials shown above.
