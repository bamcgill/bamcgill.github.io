---
title: "Application Migration - Part 1"
date: 2012-03-06 12:28:00 +0000
last_modified_at: 2012-03-06 12:28:43 +0000
---

For the last couple of releases SQLDeveloper has added features which help our users analyze their applications.  Now, when I say analyze, I really just mean search the application code for items of interest which either need to be reported on, or need to be changed to work with Oracle.  
  
  
This feature within the migration capabilities  allows you to look at application code and search it for particular items that are of interest. Lets take a very simple example of what we want to look at.  I'm using a sample shell script to use isql to get some data from sybase.  
  

```
#!/bin/sh
isql -UMYUSER -PMYPASS -SMYSERVER <<EOF
use pubs2
go
select count(*) from authors
go
select top 5 au_lname,au_fname,postalcode from authors
go
EOF
```

  
  
Running this in sybase using pubs2 gives us these results.  
  
  

```
bash-3.2$ sh test.sh
             
 ----------- 
          23 

(1 row affected)
 au_lname                                 au_fname             postalcode 
 ---------------------------------------- -------------------- ---------- 
 White                                    Johnson              94025      
 Green                                    Marjorie             94618      
 Carson                                   Cheryl               94705      
 O'Leary                                  Michael              95128      
 Straight                                 Dick                 94609      

(5 rows affected)
```

  
  
Now, migrating this to Oracle by itself is a simple operation.  The SQL is simple and we can migrate it by hand, however, if we had many scripts like this we can use the application migration features to automate a lot of this.    
  
  
For this migration to work, we first need to migrate the database which we can do with the database migration features in SQLDeveloper.   Firstly, we use SQLDeveloper to connect to Sybase.  We can see the structure of the table for authors here.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXn3SihCUASZhHBeYIT9pTMBZhvdhTfsxoaNhOLRfC_IDX5Vch9JwK105gMRvqHH8n1H1Gllw-VMG8AKNL6k094esqmUukxsCSs0v5jMtQRlYvJaQgYB-0rvYyXw6TEvZsK1NamXfyj7w/s320/sybasepubs2.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXn3SihCUASZhHBeYIT9pTMBZhvdhTfsxoaNhOLRfC_IDX5Vch9JwK105gMRvqHH8n1H1Gllw-VMG8AKNL6k094esqmUukxsCSs0v5jMtQRlYvJaQgYB-0rvYyXw6TEvZsK1NamXfyj7w/s1600/sybasepubs2.PNG)

  
  
Next we create a migration repository in an oracle schema and migrate the pubs2 database to oracle.  When its complete, we can see the status here.  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHk2lT1iY-amJUqeu5WETjpoXWXl-E7ipMDU0uBJ5UZwU57bY5kSVvJWZiAmblBOZ2aKxB9x9uEIr0oUnHQj4qOxYWFf6IvRL2s9nITv0a4xoz06atjLI93XdtXmMMwLySvbypTIhbzAY/s400/sybasemigrationstatus.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHk2lT1iY-amJUqeu5WETjpoXWXl-E7ipMDU0uBJ5UZwU57bY5kSVvJWZiAmblBOZ2aKxB9x9uEIr0oUnHQj4qOxYWFf6IvRL2s9nITv0a4xoz06atjLI93XdtXmMMwLySvbypTIhbzAY/s1600/sybasemigrationstatus.PNG)

  
  
Now we have the database moved to oracle, we can see the tables and data when we create a connection to the new schema for dbo, which by default is called dbo\_pubs2.  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiOa9S8OxwDXFjpoUWEXepcF8kFY6uXHwIaXj7j3vhc5SoAGK1wPgHMgvEopZ6nqq4-XjEy8TF_Bbu4yvkaPASKPvxM_fNx5NOpAUlF4V-5URRS9fdwjtcXB9eIH6VIQwxvHb7YP5flEGE/s400/pubs2data.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiOa9S8OxwDXFjpoUWEXepcF8kFY6uXHwIaXj7j3vhc5SoAGK1wPgHMgvEopZ6nqq4-XjEy8TF_Bbu4yvkaPASKPvxM_fNx5NOpAUlF4V-5URRS9fdwjtcXB9eIH6VIQwxvHb7YP5flEGE/s1600/pubs2data.PNG)

  
  
Now, when we migrate the application and run it against oracle, we have a database and data to use.  
So, in a perfect world, we can get the application to run out of the box after migration.  Lets manually rewrite this and see what it looks like.  
  
  

```
#!/bin/sh

sqlplus dbo_pubs2/dbo_pubs2 << EOF

select count(*) from authors;

select au_lname, au_fname, postalcode from authors where rownum <=5;

EOF
```

  
and running this against our migrated database gives us this output.  

```
ORACLE>sh test.sh

SQL*Plus: Release 11.2.0.1.0 Production on Tue Mar 6 12:24:29 2012

Copyright (c) 1982, 2009, Oracle.  All rights reserved.

Connected to:
Oracle Database 11g Enterprise Edition Release 11.2.0.1.0 - 64bit Production
With the Partitioning, OLAP, Data Mining and Real Application Testing options

SQL> SQL> 
  COUNT(*)
----------
        23

SQL> SQL> 
AU_LNAME                                 AU_FNAME             POSTALCODE
---------------------------------------- -------------------- ----------
White                                    Johnson              94025
Green                                    Marjorie             94618
Carson                                   Cheryl               94705
O'Leary                                  Michael              95128
Straight                                 Dick                 94609

SQL> SQL> Disconnected from Oracle Database 11g Enterprise Edition Release 11.2.0.1.0 - 64bit Production
With the Partitioning, OLAP, Data Mining and Real Application Testing options
ORACLE>
```

  
  
So at this stage, the we have a migrated database, and we also have a mockup of what we want our application changes to be for changing the application.  In the next post, Application Migration - Part 2, we'll look at migrating the script using the application migration features of SQL Developer to change the sql and the call to isql.
