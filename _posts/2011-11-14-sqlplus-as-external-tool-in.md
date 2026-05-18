---
title: "SQLPLus as an external tool in SQLDeveloper"
date: 2011-11-14 15:20:00 +0000
last_modified_at: 2011-11-14 15:46:31 +0000
tags:
  - external tools
  - sqlplus
  - SQL*Plus
  - SQL Developer
---

@thatjeffsmith asked me today about running SQL\*Plus from SQLDeveloper for his current sql file.  This has been shown before, but there is a simple way to add it and to get it to run your file under SQL\*Plus.  
  
The only caveate on this example, is that we are using the bequeath adapter to connect to a local XE database. You can amend this to add a service after the username  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgR8We8Iiwhz2Aao1Eav3JPez4dSQqw16xQVtvrPb1Evrq8vFtIe6Ar9d9LVtErWDoOBk9g3YqrujbpWqWGejI8ad8WO6bKT2HKEj41lN0gJbWcTjra5SGIsziSpb45l78i_tj7ZJcdVm4/s320/externalplus.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgR8We8Iiwhz2Aao1Eav3JPez4dSQqw16xQVtvrPb1Evrq8vFtIe6Ar9d9LVtErWDoOBk9g3YqrujbpWqWGejI8ad8WO6bKT2HKEj41lN0gJbWcTjra5SGIsziSpb45l78i_tj7ZJcdVm4/s1600/externalplus.PNG)

  
The main steps are to point the program executable to your SQLPlus, which will populate the executable and the Run directory.  Next you need to populate the arguments, which for sqlplus are like this.  
  
 sqlplus [LOGIN} @{FILENEMAME]  
  
where LOGIN can be any of this.  
  
  
 {[/][@] | / }  
 [AS {SYSDBA | SYSOPER | SYSASM}] [EDITION=value]  
  
  
So, our arguments will be  
  

```
${sqldev.dbuser}/${promptl:label=Password} @${file.dir}/${file.name}
```

  
You can check the variables you can submit with the insert button.  I am choosing a labelled prompt for the password here for security.  
  
Once we have all that done we can see our External tool in the list of tools.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgs2DOgPrB1PzrFr0SvrKcsCeRlOWlvAfsckYRNqav_DurQDWtOXdiFuh2sXqCl-5Sb6ZiG2eWsvoO4B_xJRs5XJA3lvdfGirjocyaeJ-xAQ7uwvZyZ9gzCmnq705rSYqPeDsclt5joj5Q/s320/externaltoolslist.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgs2DOgPrB1PzrFr0SvrKcsCeRlOWlvAfsckYRNqav_DurQDWtOXdiFuh2sXqCl-5Sb6ZiG2eWsvoO4B_xJRs5XJA3lvdfGirjocyaeJ-xAQ7uwvZyZ9gzCmnq705rSYqPeDsclt5joj5Q/s1600/externaltoolslist.PNG)

  
Now, all we have to do is make sure our file is in focus and click the SQL\*Plus button.  This will run the file with the current user of the connection we have on the file and prompt for the password.  
  
My File looks like this  

```
clear screen
select username from all_users where username like 'B%';
```

  
and running it with my new SQL\*Plus button gives me this.  
  

```
C:\oraclexe\app\oracle\product\11.2.0\server\bin>
C:\oraclexe\app\oracle\product\11.2.0\server\bin\sqlplus.exe barry/barry "@C:\Documents and Settings\bamcgill\Desktop/Untitled1.sql"

SQL*Plus: Release 11.2.0.2.0 Beta on Mon Nov 14 15:38:25 2011

Copyright (c) 1982, 2010, Oracle.  All rights reserved.

Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - Beta

 

USERNAME
------------------------------
BARRY
BARRY2

SQL>
```

  
Now, thats not so secure either, since you can see my password, so we want to switch off banner output too which will suppress the login string and the header.  You can do this by editing your external tools and adding it to the arguments like this.  

```
-S ${sqldev.dbuser}/${promptl:label=Password} @${file.dir}/${file.name}
```

  
giving you what you want here.  

```
C:\oraclexe\app\oracle\product\11.2.0\server\bin>
C:\oraclexe\app\oracle\product\11.2.0\server\bin\sqlplus.exe -S barry/barry "@C:\Documents and Settings\bamcgill\Desktop/Untitled1.sql"
 

USERNAME
------------------------------
BARRY
BARRY2
```
