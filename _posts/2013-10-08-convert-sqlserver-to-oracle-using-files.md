---
title: "Convert SQLServer to Oracle using files - Part 3"
date: 2013-10-08 01:23:00 +0000
last_modified_at: 2013-10-08 08:35:34 +0000
tags:
  - SQL Server
  - Migration
  - SQL Developer
  - DDL generation
---

In [part 1](http://barrymcgillin.blogspot.co.uk/2013/10/convert-sql-server-to-oracle-using.html) we generated the offline capture scripts to take to the SQL Server machine, unloaded the metadata, zipped it up and copied it back to out local machine. In [part 2](http://barrymcgillin.blogspot.co.uk/2013/10/convert-sql-server-to-oracle-using_7.html) we used SQL Developer to create a migration project and load the capture files into SQL Developer.  We then converted the metadata into its Oracle equivalent.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjF_deYbiNZUBmPqjTTQaVFKZYshHaAN6DnB3mUxGNUNc-S6emWbPMoLpmuZdwtLCnfNT6buCx50sKHX2ds29pa7DIdLKjL5BfofOhXxwuio2JGVfLnZ1YVIaYVZLznLN4Gp4ohhRiCaLQ/s1600/Screen+Shot+2013-10-07+at+23.58.37.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjF_deYbiNZUBmPqjTTQaVFKZYshHaAN6DnB3mUxGNUNc-S6emWbPMoLpmuZdwtLCnfNT6buCx50sKHX2ds29pa7DIdLKjL5BfofOhXxwuio2JGVfLnZ1YVIaYVZLznLN4Gp4ohhRiCaLQ/s1600/Screen+Shot+2013-10-07+at+23.58.37.png)

In this episode we will try and generate DDL from our migration project.  Right now, We can see the Oracle objects in the Converted Database Objects node.  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgxGzA_nwI2X17zhC6gAQj2zYVI_zBlRRiDIzR2PwOw3KXkQ4a5HUQocsjCL3f1QempKqlqP8QZz-HemLH970QJu7OTuxhUoYBsVb20gIMYYgv9B2ugXV6Ez7lSyVkKZJGwgQHo-Lqqrqc/s1600/Screen+Shot+2013-10-08+at+00.03.22.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgxGzA_nwI2X17zhC6gAQj2zYVI_zBlRRiDIzR2PwOw3KXkQ4a5HUQocsjCL3f1QempKqlqP8QZz-HemLH970QJu7OTuxhUoYBsVb20gIMYYgv9B2ugXV6Ez7lSyVkKZJGwgQHo-Lqqrqc/s1600/Screen+Shot+2013-10-08+at+00.03.22.png)If we right click on Converted Database objects and choose generate, we can generate DDL to create the Oracle Schema and Objects.  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjktcwCkkIFvvVoRRa9ufi2PZ6UsvJdOeA46rtYvoUYUnaUb07y4_8HwPs-dPiYYinnMt3UPHoHspkhAqsu-AhzMQ0amoQbPHAFhcFR7oWtZsSJ0uGNuJIpHcRiuVYOOj2L8efzfOezTeo/s1600/Screen+Shot+2013-10-08+at+00.03.34.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjktcwCkkIFvvVoRRa9ufi2PZ6UsvJdOeA46rtYvoUYUnaUb07y4_8HwPs-dPiYYinnMt3UPHoHspkhAqsu-AhzMQ0amoQbPHAFhcFR7oWtZsSJ0uGNuJIpHcRiuVYOOj2L8efzfOezTeo/s1600/Screen+Shot+2013-10-08+at+00.03.34.png)The wizard appears again with the introduction screen.  Clicking next takes us directly to the Target database Screen.  
  
  

Click on offline to choose generation of files.  For specifics of how the files get generated, click on advanced options

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjC0vohArihT6qFOJDNr-lp__QXV11x4XEyujkfvtIw_SlcQZMmwmyp-6zMh4ICiEF-RNHDICtmWC6rmBfPSYq_gpasFvUqL5IaMn9YfVJkA4R4MrbszZjotdHtBCrkChnJPXZDSov8hZQ/s1600/Screen+Shot+2013-10-08+at+00.04.11.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjC0vohArihT6qFOJDNr-lp__QXV11x4XEyujkfvtIw_SlcQZMmwmyp-6zMh4ICiEF-RNHDICtmWC6rmBfPSYq_gpasFvUqL5IaMn9YfVJkA4R4MrbszZjotdHtBCrkChnJPXZDSov8hZQ/s1600/Screen+Shot+2013-10-08+at+00.04.11.png)

 You can select what way you want to generate your files, all in one file, a file per object type or a file per object. You can also choose the types of objects you want to generate and run.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg_rCJ433oKm8gQc5iFeGqBHZKippXDPbilA4a5pMZkGcnv_gS6XWx6xO9t83Kk4nduob_OXAlKO2l9MJ9eI4w5LFsDAB_bwLW8AAOMX8Sy47JhQOxxq6LE57YtGJ_QQBnuaKxtcW22p64/s1600/Screen+Shot+2013-10-08+at+00.04.45.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg_rCJ433oKm8gQc5iFeGqBHZKippXDPbilA4a5pMZkGcnv_gS6XWx6xO9t83Kk4nduob_OXAlKO2l9MJ9eI4w5LFsDAB_bwLW8AAOMX8Sy47JhQOxxq6LE57YtGJ_QQBnuaKxtcW22p64/s1600/Screen+Shot+2013-10-08+at+00.04.45.png)

 In this demo, I will just generate tables, data and supporting objects.   Clicking next  will take us to the data move page where we again choose offline to generate files.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiOiEhcPUL9gIzmmC9KVbZ3drcPiMXGrredY5Z4WE1NfsJjPufYhT3O8XFUAlPJmyf2HFcDF0o_oGS6aUGavparJQ4JI0Ulcg5-lPrYZ7bZ1uD5eXHR1VNESWBQ0uMdJ2deB7sJR9RxrVQ/s1600/Screen+Shot+2013-10-08+at+00.05.26.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiOiEhcPUL9gIzmmC9KVbZ3drcPiMXGrredY5Z4WE1NfsJjPufYhT3O8XFUAlPJmyf2HFcDF0o_oGS6aUGavparJQ4JI0Ulcg5-lPrYZ7bZ1uD5eXHR1VNESWBQ0uMdJ2deB7sJR9RxrVQ/s1600/Screen+Shot+2013-10-08+at+00.05.26.png)

 Choosing advanced options allows us to be specific about date masks and delimiters for data unload.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhkpJ0nxxE2H4kdpr-o7bWB97LUnSC0jhzLEUUDAdfxkbWU_7lekV_pB-GeGzrXsitiq2h4COw0uSG3Un9g58TLHKJSyKN4X-6FJP2q-uoijRcIV_oeiM84vUkiScyPrSMvjweSFRUIE4E/s1600/Screen+Shot+2013-10-08+at+00.05.39.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhkpJ0nxxE2H4kdpr-o7bWB97LUnSC0jhzLEUUDAdfxkbWU_7lekV_pB-GeGzrXsitiq2h4COw0uSG3Un9g58TLHKJSyKN4X-6FJP2q-uoijRcIV_oeiM84vUkiScyPrSMvjweSFRUIE4E/s1600/Screen+Shot+2013-10-08+at+00.05.39.png)

 Once we have chosen our options, we click next and review the summary.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyR3XUnu2b-sWvaxnsI58K9zhIfSyckh7lbBJf4Y5Y_j6GtUGmNqWGWOHxCstLZvd0XqfIIeT5d_3dBkIwUUyrixNQIRREgg6WXCq2ShdyKWfqrZTC6yZWRJfgvWuwfvfQ3dFRdv7J-rw/s1600/Screen+Shot+2013-10-08+at+00.07.10.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyR3XUnu2b-sWvaxnsI58K9zhIfSyckh7lbBJf4Y5Y_j6GtUGmNqWGWOHxCstLZvd0XqfIIeT5d_3dBkIwUUyrixNQIRREgg6WXCq2ShdyKWfqrZTC6yZWRJfgvWuwfvfQ3dFRdv7J-rw/s1600/Screen+Shot+2013-10-08+at+00.07.10.png)

 Finally, we click finish and the files are generated in the output directory we specified when setting up the project in part 2.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEifX1U8bvCTbJ3uHNPikIMnZLbAW-F3xIFAADL-iDUUnhx8wXKQaVtiTgFGbrhN_1v42JYWmvpcRA9owVTXSSai9Nn-xvBB2Te9_W50dYvukjoAneILMPJ3Mix0z2Q_t7QHt_1p5awnAoA/s1600/Screen+Shot+2013-10-08+at+00.08.17.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEifX1U8bvCTbJ3uHNPikIMnZLbAW-F3xIFAADL-iDUUnhx8wXKQaVtiTgFGbrhN_1v42JYWmvpcRA9owVTXSSai9Nn-xvBB2Te9_W50dYvukjoAneILMPJ3Mix0z2Q_t7QHt_1p5awnAoA/s1600/Screen+Shot+2013-10-08+at+00.08.17.png)

Now, Lets go see what we generated.  If we go to the output directory we specified in the project, we can see the list of files we generated.  Remember the options we chose for generation.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiSp7Ptm_10YwfgJI90gKO-KssJtK4r6PVmZl_OktwypyFFuAFNs2o4EQETO4Lb4Xuard5PHUwOQEWjQ40DUhFHnIZZnF6LwWfebAvQsNx3ca7pI9vz3Z09GzXkXMMENOIB7Fx1WDlQGYo/s1600/Screen+Shot+2013-10-08+at+00.56.32.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiSp7Ptm_10YwfgJI90gKO-KssJtK4r6PVmZl_OktwypyFFuAFNs2o4EQETO4Lb4Xuard5PHUwOQEWjQ40DUhFHnIZZnF6LwWfebAvQsNx3ca7pI9vz3Z09GzXkXMMENOIB7Fx1WDlQGYo/s1600/Screen+Shot+2013-10-08+at+00.56.32.png)

We also get the master.sql file opened in SQL Developer which looks like this

```
SET ECHO OFF
SET VERIFY OFF
SET FEEDBACK OFF
SET DEFINE ON
CLEAR SCREEN
set serveroutput on

COLUMN date_time NEW_VAL filename noprint;
SELECT to_char(systimestamp,'yyyy-mm-dd_hh24-mi-ssxff') date_time FROM DUAL;
spool democapture_&filename..log

-- Password file execution
@passworddefinition.sql

PROMPT Creating Role
@role.sql

prompt creating user Emulation
@@Emulation/user.sql

prompt creating user dbo_Northwind
@@dbo_Northwind/user.sql

prompt creating user dbo_pubs
@@dbo_pubs/user.sql

prompt Building objects in Emulation
@@Emulation/master.sql

prompt Building objects in dbo_Northwind
@@dbo_Northwind/master.sql

prompt Building objects in dbo_pubs
@@dbo_pubs/master.sql
```

  
Now, lets try and run this file and create the users and objects.  Firstly, we choose a connection to run the script.  This user must have the privileges to create users and all their ancillary objects.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgekMAKR02E39UyJ4SMQ5_gXd4nFBqZSLchx4e52Tfc9UPcf3h0T4idCqVi3DnRmoQhGpeYXV23P6G7wrPb5HOZv5NISQp5f9hmKGyuSa8K9o9sc9xSGXmDDocam26v7GhHEYGH_21WwWI/s1600/Screen+Shot+2013-10-08+at+01.13.45.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgekMAKR02E39UyJ4SMQ5_gXd4nFBqZSLchx4e52Tfc9UPcf3h0T4idCqVi3DnRmoQhGpeYXV23P6G7wrPb5HOZv5NISQp5f9hmKGyuSa8K9o9sc9xSGXmDDocam26v7GhHEYGH_21WwWI/s1600/Screen+Shot+2013-10-08+at+01.13.45.png)

We can run this script to create the users.  Notice the worksheet output showing the output of the files.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiet38-lYCfe1boW3pQtTD8QeAjtzKcizuKxRy4Ues8LoV87msWJHMxfxJ4C79_avbAJU6h5WYLBzC1hCLfgkjk0vSK0eBQbl6b8jAcdRehW_Rp1HjSAGEopi6nvC8DWJwaBwZnwPrJMRs/s1600/Screen+Shot+2013-10-08+at+01.59.30.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiet38-lYCfe1boW3pQtTD8QeAjtzKcizuKxRy4Ues8LoV87msWJHMxfxJ4C79_avbAJU6h5WYLBzC1hCLfgkjk0vSK0eBQbl6b8jAcdRehW_Rp1HjSAGEopi6nvC8DWJwaBwZnwPrJMRs/s1600/Screen+Shot+2013-10-08+at+01.59.30.png)

Once this is complete, we can create a connection in SQL Developer to one of the users created, dbo\_Northwind, dbo\_pubs and emulation.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRzAZ9IReM0oPUvbq1-fRq6m5y5ozG63giQkjORbTqTmQf4UVE6sbg5yrbNRzdA3uirOxzklv-n7ybNfXTctIBq1hgZtifchJilPgXudsGg0lJmQcMUZnak4ArrA6sdM5jeq5HS9k5cEk/s1600/Screen+Shot+2013-10-08+at+02.06.27.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRzAZ9IReM0oPUvbq1-fRq6m5y5ozG63giQkjORbTqTmQf4UVE6sbg5yrbNRzdA3uirOxzklv-n7ybNfXTctIBq1hgZtifchJilPgXudsGg0lJmQcMUZnak4ArrA6sdM5jeq5HS9k5cEk/s1600/Screen+Shot+2013-10-08+at+02.06.27.png)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgfQaO7TQcHDVkCcFqteiTqoob2KWPG3jCtsh0CTrFCaHzvzaSSP6uB0X-1qKBkGCBZVpVGLbd9oNOMvuEmn8rUMDkIRlpExZEs6cmfkHVkNSd3ltfOMHpDRNR0_Bq5st5bv4NCHVvucqY/s1600/Screen+Shot+2013-10-08+at+02.09.13.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgfQaO7TQcHDVkCcFqteiTqoob2KWPG3jCtsh0CTrFCaHzvzaSSP6uB0X-1qKBkGCBZVpVGLbd9oNOMvuEmn8rUMDkIRlpExZEs6cmfkHVkNSd3ltfOMHpDRNR0_Bq5st5bv4NCHVvucqY/s1600/Screen+Shot+2013-10-08+at+02.09.13.png)

Now, we have created the schema from the DDL which was generated.  In the next and final episode of this, we will visit the data move.  We will run the data move scripts on SQL Server and extract the data which we can load via SQL Loader or external tables.
