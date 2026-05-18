---
title: "Connecting SQLcl to MySQL"
date: 2018-06-11
tags:
  - oracle
  - SQLDEVELOPER
  - MySQL
  - sqlcl
---

This is very easy since we already support copy to oracle in SQLDeveloper.  The functionality for copying  tables and data from a connection to another connection is pretty straight forward.

First you need to download the [MySQL Connector JDBC driver](https://dev.mysql.com/downloads/connector/j/). Explode it out and take the jdbc driver and put it into your SQLcl/lib directory/drivers directory.

Now, startup sqlcl.  If you start with /nolog, you can see which drivers are loaded.

$ sql /nolog

SQLcl: Release 18.3 Production on Mon Jun 11 13:36:16 2018

Copyright (c) 1982, 2018, Oracle.  All rights reserved.

SQL>

try 'show java' which will find out whats on the class path. (output shortened for brevity)

SQL> show java

Java Detail

-----------

java.home= /L../J./J.../jdk.../Contents/Home/jre

java.vendor= Oracle Corporation

java.vendor.url= http://java.oracle.com/

java.version= 1.8.0\_161

user.dir=/Users/bamcgill/work/sqlcl/

user.home= /Users/bamcgill

user.name= bamcgill

------------------------------------------------------------------------

SQL\_HOME=/Users/bamcgill/work/sqlcl

------------------------------------------------------------------------

Classpath

$SQL\_HOME/lib/dbtools-sqlcl.jar

**$SQL\_HOME/lib/drivers/mysql-connector-java-8.0.11.jar**

...(all the other jars)

SQL>

Now we can do a JDBC connection like normal on SQLcl but using the connect statement

connect jdbc:mysql://localhost:3306/world?user=root

which will connect to the world database as the root user.

If you have other parameters that you want to set, then you will need to make sure that scan or define is off as we need to use '&' in the url to add other parameters

SQL> set define off

SQL> connect jdbc:mysql://localhost:3306/world?user=root&useSSL=false

Connected.

SQL>

cool.  Now we can use standard mysql commands in SQLcl.

SQL> show databases;

SCHEMA\_NAME

----------------------------------------------------------------

information\_schema

employees

mysql

performance\_schema

sakila

sakilla

sys

world

8 rows selected.

SQL> use world;

World succeeded.

SQL> show tables;

TABLE\_NAME

----------------------------------------------------------------

city

country

countrylanguage

SQL>

and finally, do some normal SQL as well :)

SQL> select city.name from country, city

2  where country.code=city.countrycode

3\* and country.name='Ireland';Name

-----------------------------------

Dublin

Cork

SQL>
