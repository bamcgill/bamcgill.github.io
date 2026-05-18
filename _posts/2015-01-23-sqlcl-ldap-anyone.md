---
title: "SQLCl - LDAP anyone?"
date: 2015-01-23 15:02:00 +0000
last_modified_at: 2015-01-23 15:02:16 +0000
tags:
  - oracle
  - sqlplus
  - sqlcl
  - SQLDEVELOPER
---

since  we released our first preview of SDSQL, we've made  a lot of changes to it and enhanced a lot of things too in there so it would be more useable.  One specific one was the use of LDAP which some customers on SQLDeveloper are using in their organisations as a standard and our first release precluded them from working with this.  
  
Well, to add this, we wanted a way that we could specify the LDAP strings and then use them in a connect statement.  We introduced a command called SET LDAPCON for setting the LDAP connection.  You can set it like this at the SQL> prompt  

```
 set LDAPCON jdbc:oracle:thin:@ldap://scl58261.us.oracle.com:389/#ENTRY#,cn=OracleContext,dc=ldapcdc,dc=lcom
```

  
or set it as an environment variable  

```
 (~/sql) $export LDAPCON=jdbc:oracle:thin:@ldap://scl58261.us.oracle.com:389/#ENTRY#,cn=OracleContext,dc=ldapcdc,dc=lcom
```

  
Then you can come along and as long as you know your service name, we're going to swap out the ENTRY delimiter in the LDAP connection with your service.  We're working on a more permanent way to allow these to be registered and used so they are more seamless.  
  
In the meantime, you can then connect to your LDAP service like this  

```
 BARRY@ORCL>set LDAPCON jdbc:oracle:thin:@ldap://scl58261.us.oracle.com:389/#ENTRY#,cn=OracleContext,dc=ldapcdc,dc=lcom  
 BARRY@ORCL>connect barry/oracle@orclservice_test(Emily's Desktop)  
 Connected  
 BARRY@PDBOH12>tables  
 Command=tables  
 TABLES   
 TEST
```

  
Here's a qk little video of it in action!  You can then use  the 'SHOW JDBC' command to show what you are connected to.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhJ61sHpgs80C6pGDobJ8IiSioj8YWtv1rzZIOhcOrtNnkZ3VsdwfO7lIlmf-ixq5uwcNnONKJqCiggMX7W3GhRo2pCNzJryq3Fu2YNnGFI5iBvd2gUKII0C4LYHkWxiw8Yh7vAjUTn9_o/s1600/2015-01-23+14_30_03.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhJ61sHpgs80C6pGDobJ8IiSioj8YWtv1rzZIOhcOrtNnkZ3VsdwfO7lIlmf-ixq5uwcNnONKJqCiggMX7W3GhRo2pCNzJryq3Fu2YNnGFI5iBvd2gUKII0C4LYHkWxiw8Yh7vAjUTn9_o/s1600/2015-01-23+14_30_03.gif)

  
This is the latest release which should be online soon, and you  can download it from [here](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/sqldev-41ea-2372780.html).  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjUoY3e8HeuVX5UFwTUFuky-7bM3hA6bLrIuXgCTvc6k3nQe-8OJ9GLm6IM4nz8vMy8L-U6D-0RRPGC0mNxI6PTrUvAy-6xIGk5RJZbtuhO3ejpGX7hW5yT3XdiBvffFoDPHtQIFLDjEqA/s1600/SQL_Developer_4_1_Early_Adopter.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjUoY3e8HeuVX5UFwTUFuky-7bM3hA6bLrIuXgCTvc6k3nQe-8OJ9GLm6IM4nz8vMy8L-U6D-0RRPGC0mNxI6PTrUvAy-6xIGk5RJZbtuhO3ejpGX7hW5yT3XdiBvffFoDPHtQIFLDjEqA/s1600/SQL_Developer_4_1_Early_Adopter.png)
