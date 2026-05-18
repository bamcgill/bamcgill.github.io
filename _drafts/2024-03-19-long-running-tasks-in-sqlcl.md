---
title: "Long Running tasks in SQLcl"
date: 2024-03-19
---

With our latest release of SQLcl version 24.1.0,

```
 blogger> sql /nolog  
 SQLcl: Release 24.1 Production on Tue Mar 19 22:40:00 2024  
 Copyright (c) 1982, 2024, Oracle. All rights reserved.  
 SQL> version  
 Oracle SQLDeveloper Command-Line (SQLcl) version: 24.1.0.0 build: 24.1.0.079.1942  
 SQL>
```

we've added a way to run multiple tasks in parallel.  You can run any sqlcl command in the background that makes sense.   We've introduced 3 commands that work together.

1. Background - Takes a command and runs it as a background task
2. Jobs - Lists and manages  the commands that have been run with background, and
3. wait4 - This is an explicit command to either wait for a period of time in milliseconds or wait for a task ir list of tasks to finish

```
 SQL> help background syntax  
  background|bg [-wait4|-w4 <wait4>] [-taskname|-tn <taskname>] <commandspec>  
 SQL>
```

This shows that we can name the task and wait for another task to complete, and include a full command with its options.  This command allow all sqlcl and sqlplus style commands. Take this liquibase command as an example which generates a changeset for a table

```
 SQL> connect -name blog  
 Connected.  
 SQL> liquibase generate-db-object -object-name employees -object-type table -sql  
 --Starting Liquibase at 2024-03-19T23:10:47.345715 (version 4.26.0 #1141 built at 2024-02-06 21:31+0000)  
 Changelog created and written out to file employees_table_1.xml   
 Operation completed successfully.  
 SQL>
```

This command can also be run in the background as well.  Here's a simple example

```
 SQL> jobs   
 No tasks available.  
 SQL> background -taskname lb-generate-hr liquibase generate-db-object -object-name employees -object-type table -sql  
 Started task with id: 2  
 SQL> jobs  
  2: [ Running ] lb-generate-hr (/Users/bamcgill/.sqlcl/jobslogs/lbgeneratehr.log)  
 SQL> jobs logs -id 2  
 --Starting Liquibase at 2024-03-19T23:21:09.669189 (version 4.26.0 #1141 built at 2024-02-06 21:31+0000)  
 Changelog created and written out to file employees_table_3.xml   
 Operation completed successfully.  
 SQL> jobs  
  2: [ Finished ] lb-generate-hr (/Users/bamcgill/.sqlcl/jobslogs/lbgeneratehr.log)  
 SQL>
```

Here, we took the liquibase command we ran earlier, and called it from background, giving it the name lb-generate-hr'  We used the command  'jobs' to list the commands and the 'jobs logs -id 2 ' to list the logs of the command, which show the command ran exactly like it did in the normal command.

There
