---
title: "Scanning Applications"
date: 2011-06-17 17:00:00 +0000
last_modified_at: 2011-06-17 18:06:03 +0000
tags:
  - Migration Workbench SQL Developer
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi5jIi4bLoE8HWmQwhFP5C2elXKJtDiy1q9B4SuYbuZEaSfOU9kO76Zy6s_WodIj9gmem_TgRfBZ5J7m9QKnMT7oVNmPmGypY7Cjd7T3Gfwm0RJFvtvVC0dtmGg1dq9fYGLIrzcHAM-YkQ/s200/appscan1.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi5jIi4bLoE8HWmQwhFP5C2elXKJtDiy1q9B4SuYbuZEaSfOU9kO76Zy6s_WodIj9gmem_TgRfBZ5J7m9QKnMT7oVNmPmGypY7Cjd7T3Gfwm0RJFvtvVC0dtmGg1dq9fYGLIrzcHAM-YkQ/s1600/appscan1.PNG)  
When re-platforming any application, there are specific things that must be changed in order to make that application work on the new platform. Database migration has been available in SQL Developer since 1.2. However, this is only part of the process of changing an application.

In SQL Developer 3.0, we introduced the ability to scan application source code for items of interest that required migration. We call these items rules. These rules are defined in a simple XML format. We have included rules for Sybase CT and DB lib client applications by default.

In 3.1 we extended the support for applications and have opened up the rules API so that a rule can be specified for any type of file. We have included a mechanism to recognize files with and without extensions so we only apply rules appropriate to the file type.

This produces a nice summary of the contents of the application, no matter what source is used. As you can see each rule is made is made up of a regular expression. Each rule is applied to the file and the results aggregated and summarized by type, call and volume.

High Level Overview

-------------------

63 total calls found

43 distinct calls found

8 files scanned

8 language types

12 total files in source

443 lines of code in scanned application

-------------------------------------------------------------

File Type Summary

----------------------

perl 1 file

sql 1 file

c 2 files

php 1 file

java 1 file

ksh 2 files

asp 1 file

specialized 1 file

-------------------------------------------------------------

As we get closer to release we can take a closer look at how we can replace some of the things we found automatically.
