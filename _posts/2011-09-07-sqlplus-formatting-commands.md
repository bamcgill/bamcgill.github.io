---
title: "SQL*Plus Formatting Commands"
date: 2011-09-07 14:48:00 +0000
last_modified_at: 2011-09-13 13:51:51 +0000
tags:
  - reports
  - SQL*Plus
  - worksheet
  - formatting
  - SQL Developer
  - Oracle XE
---

Since the last post on SQL\*Plus commands was completed, we have also added more functionality to the SQL Developer's SQL\*Plus support.    
  Specifically, we've added some formatting reports to help the folks who have tons of plus reports running for various things. These features will be a part of the next major release of SQL Developer. Lets have a look and see whats supported.   

It might be easier to tell you whats not supported now. Its 'break' and 'sum'. Most other SQLPlus formatting is now supported. So, lets take a look and see how it looks.  

These features will be available in the next release of SQL Developer.

In SQL Developer, as you add SQL\*plus command, they stay around for the lifetime of your worksheet, just like SQL\*Plus unless you get rid of them. To Clear all your column formatting just use

```
clear columns
```

Now we've a clean setup and ready to start.  As usual, if you want to see what settings are in force, you can issue the command:

```
show all
```

which will give you the usual list of suspects as you have seen before [here](http://barrymcgillin.blogspot.com/2011/07/sqlplus-commands.html).  With formatting now, there are a few more.  We'll see those shortly when we do a little bit of formatting.  Using the standard HR schema in XE, a simple query on the employees table  

```
select * from employees where rownum < 5;
```

gives us this  

```
EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE                JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID
----------- -------------------- ------------------------- ------------------------- -------------------- ------------------------ ---------- ---------- -------------- ---------- -------------
        100 Steven               King                      SKING                     515.123.4567         17-JUN-03                AD_PRES         24000                                      90 
        101 Neena                Kochhar                   NKOCHHAR                  515.123.4568         21-SEP-05                AD_VP           17000                       100            90 
        102 Lex                  De Haan                   LDEHAAN                   515.123.4569         13-JAN-01                AD_VP           17000                       100            90 
        103 Alexander            Hunold                    AHUNOLD                   590.423.4567         03-JAN-06                IT_PROG          9000                       102            60 

 4 rows selected
```

  
  
Lovely, right?  Of course, but we could do better.  So, lets remove the columns we're not interested in using the column noprint option.
  
  
  

```
column employee_id noprint
column job_id noprint
column commission_pct noprint
column manager_id noprint
column department_id noprint
select * from employees where rownum < 5;
```

  
  
which now gives us this.
  
  
  

```
FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE                    SALARY 
-------------------- ------------------------- ------------------------- -------------------- ------------------------ ---------- 
Steven               King                      SKING                     515.123.4567         17-JUN-03                     24000 
Neena                Kochhar                   NKOCHHAR                  515.123.4568         21-SEP-05                     17000 
Lex                  De Haan                   LDEHAAN                   515.123.4569         13-JAN-01                     17000 
Alexander            Hunold                    AHUNOLD                   590.423.4567         03-JAN-06                      9000 

 4 rows selected
```

  
  
Ok, its looking better, but theres a lot of white space in there.  Lets take that out.
  
  
  

```
column employee_id noprint
column job_id noprint
column commission_pct noprint
column manager_id noprint
column department_id noprint
column first_name format a10 
column last_name format a7 
column email format a8 
column hire_date format a10 
select * from employees where rownum < 5;
```

  
  
which now looks a lot tidier.  
  
  

```
FIRST_NAME LAST_NA EMAIL    PHONE_NUMBER         HIRE_DATE      SALARY 
---------- ------- -------- -------------------- ---------- ---------- 
Steven     King    SKING    515.123.4567         17-JUN-03       24000 
Neena      Kochhar NKOCHHAR 515.123.4568         21-SEP-05       17000 
Lex        De Haan LDEHAAN  515.123.4569         13-JAN-01       17000 
Alexander  Hunold  AHUNOLD  590.423.4567         03-JAN-06        9000 

 4 rows selected
```

  
  
Now, this fits nicely in to the page and we can also make the separators and titles a little fancier
  
  
  

```
clear columns
set colsep "|"
column employee_id noprint
column job_id noprint
column commission_pct noprint
column manager_id noprint
column department_id noprint
column first_name format a10 heading "First|Name"
column last_name format a7 heading "Last|Name"
column email format a8 heading "Email"
column hire_date format a10 heading "Hired"
column phone_number format a12 heading "Phone"
column salary format $999,999 heading "Salary"
select * from employees where rownum < 5;
```

  
  
resulting in this
  
  
  

```
First     |Last   |        |            |          |             
Name      |Name   |Email   |Phone       |Hired     |    Salary 
---------- ------- -------- ------------ ---------- ---------- 
Steven    |King   |SKING   |515.123.4567|17-JUN-03 |   $24,000
Neena     |Kochhar|NKOCHHAR|515.123.4568|21-SEP-05 |   $17,000
Lex       |De Haan|LDEHAAN |515.123.4569|13-JAN-01 |   $17,000
Alexander |Hunold |AHUNOLD |590.423.4567|03-JAN-06 |    $9,000

 4 rows selected
```

  
  
which spruces it up a bit.  Now, we can add titles top and bottom using standard SQL\*Plus syntax too
  
  
  

```
clear columns
CLEAR screen

set colsep "|"
column employee_id noprint
column job_id noprint
column commission_pct noprint
column manager_id noprint
column department_id noprint
column first_name format a10 heading "First|Name"
column last_name format a7 heading "Last|Name"
column email format a8 heading "Email"
column hire_date format a10 heading "Hired"
column phone_number format a12 heading "Phone"
column salary format $999,999 heading "Salary"
SET linesize 80
SET pagesize 15

ttitle LEFT '09/07/2011' RIGHT 'Page:' SQL.pno SKIP 2 CENTER 'HR REPORT' SKIP
BTITLE COL 35 'CONFIDENTIAL' ON

select * from employees where rownum < 7;
```

  
  
and our report looks like this now.
  
  
  

```
09/07/2011                                                             Page:   1
                                                                                
                                   HR REPORT                                    
First     | Last  |        |            |          |            
Name      | Name  | Email  | Phone      |  Hired   |   Salary 
---------- ------- -------- ------------ ---------- ----------
Steven    |King   |SKING   |515.123.4567|17-JUN-03 |   $24,000
Neena     |Kochhar|NKOCHHAR|515.123.4568|21-SEP-05 |   $17,000
Lex       |De Haan|LDEHAAN |515.123.4569|13-JAN-01 |   $17,000
Alexander |Hunold |AHUNOLD |590.423.4567|03-JAN-06 |    $9,000
Bruce     |Ernst  |BERNST  |590.423.4568|21-MAY-07 |    $6,000
David     |Austin |DAUSTIN |590.423.4569|25-JUN-05 |    $4,800

                                                                                
                                   CONFIDENTIAL                                 

 6 rows selected
```

  
Pretty nifty, if you've got several SQL\*Plus reports around that you need to run on SQL Developer.  Remember, like SQL\*Plus, you can check the formatting set at any time by typing   
  
  

```
column
```

giving
  

```
COLUMN  'first_name' ON
FORMAT  a10
HEADING  'First|Name' headsep '|'
JUSTIFY right

COLUMN  'hire_date' ON
FORMAT  a10
HEADING  'Hired' headsep '|'

COLUMN  'phone_number' ON
FORMAT  a12
HEADING  'Phone' headsep '|'

COLUMN  'commission_pct' ON
noprint

COLUMN  'email' ON
FORMAT  a8
HEADING  'Email' headsep '|'

COLUMN  'manager_id' ON
noprint

COLUMN  'department_id' ON
noprint

COLUMN  'last_name' ON
FORMAT  a7
HEADING  'Last|Name' headsep '|'

COLUMN  'salary' ON
FORMAT  $99,999
HEADING  'Salary' headsep '|'

COLUMN  'employee_id' ON
noprint

COLUMN  'job_id' ON
noprint
```

or
  

```
column employee_id
```

giving
  

```
COLUMN  'employee_id' ON
noprint
```

  
You can find out more about SQLDeveloper in the [usual place](http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html), and if there are features you'd like to see in the tool, submit a [Feature Request](http://sqldeveloper.oracle.com/).  If you need more details on SQL\*Plus, the latest documentation is [here](http://download.oracle.com/docs/cd/E14072_01/server.112/e10823.pdf).
