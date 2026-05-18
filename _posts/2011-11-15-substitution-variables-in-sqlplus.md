---
title: "Substitution Variables in SQL*Plus"
date: 2011-11-15 16:52:00 +0000
last_modified_at: 2011-11-16 12:04:21 +0000
tags:
  - SQL*Plus
  - define
  - Migration Workbench SQL Developer
  - scripts
  - SQL Developer
  - SQL
  - substitution variables
---

Working through security issues uncovers some interesting things. Anyone who has developed scripts for building out schemas for an application will have had the issues of passing variables to subscripts or managing password visibility when creating users, building objects or granting permissions  
  
SQLDeveloper and SQL\*Plus have substitution variables to solve this problem.  Basically, there are two types of substitution variables,  & and &&.  &foo is used to refer to the variable foo.  &&foo is also used to refer to the variable foo.  The main difference between the two variables is that first time SQL\*Plus comes across a variable defined with &&, e.g., &&foo, it prompts for the value and then uses this values for every other occurrence of the variable. &foo on the other hand will prompt for the variable, use it and then discard the value so the next time it is seen, it will prompt again.
So, now an example.  Lets assume we want to create a user db1 and db2 with some tables in each user. We can define a simple script for each one.  
  

```
define db1_password=&&db1
define db2_password=&&db2
@@users.sql
@@db1.sql
@@db2.sql
```

  
Now, this script does three things.  

1. it defines two variables for the passwords of the two users we are going to create.
2. @@users.sql sets up the users for us. Remember, in SQL\*Plus, there is only ever one connection active, so whenever you have a connect statement in your script, that will be the user running the script until you change it. In this case above, we're starting with a privileged user to create the users.
3. @@db1.sql and @@db2.sql create our users for us and we will create a table in each one. We'll see that script in a moment.

  

```
drop user user1 cascade;
prompt creating user user1
create user user1 identified by &&db1_password;
grant connect, resource to user1;
drop user user2 cascade;
prompt creating user user2
create user user2 identified by &&db2_password;
grant connect, resource to user2;
```

  
db1.sql and db2.sql are identical apart from user names.  
  

```
connect user1/&&db1
create table table1 (id number, name varchar2(10));
insert into table1 values (1,'barry');
```

  
Substitution variables are passed to any subscript called from the main script.  The initial &&db1 and &&db2 are prompted for and set to the variables db1\_password and db2\_password  
From then on, the subscripts use the variables to connect to each user.  
  
Finally, the output from all of this is below.  I have VERIFY=ON here to show the substitutions going through, but for any real world scenario, you'll want to switch that off avoid printing the passwords.  
  

```
user USER1 dropped.
creating user user1
old:create user user1 identified by &&db1_password
new:create user user1 identified by db1
user USER1 created.
grant succeeded.
user USER2 dropped.
creating user user2
old:create user user2 identified by &&db2_password
new:create user user2 identified by db2
user USER2 created.
grant succeeded.
old:connect user1/&&db1_password
new:connect user1/db1
Connected
table TABLE1 created.
1 rows inserted.
old:connect user2/&&db2_password
new:connect user2/db2
Connected
table TABLE2 created.
1 rows inserted.
Connection created by CONNECT script command disconnected
```

  
With verify off, you get cleaner output with no passwords.  If you need more ouput here, you can also use the prompt command to identify which script you are in and what is running.  
  

```
user USER1 dropped.
creating user user1
user USER1 created.
grant succeeded.
user USER2 dropped.
creating user user2
user USER2 created.
grant succeeded.
Connected
table TABLE1 created.
1 rows inserted.
Connected
table TABLE2 created.
1 rows inserted.
Connection created by CONNECT script command disconnected
```
