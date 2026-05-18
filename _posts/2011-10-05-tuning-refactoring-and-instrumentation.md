---
title: "Tuning, Refactoring and Instrumentation"
date: 2011-10-05 22:34:00 +0000
last_modified_at: 2011-10-05 22:34:14 +0000
tags:
  - Instrumentation
  - refactoring
  - Tuning
  - SQL Developer
---

For all those who attended the talk today, this is a promise partially fulfilled in that I had said I would post in more detail about the talk.  At a high level, we talked about three different topics.  Tuning, Refactoring and Instrumentation.  I'll list out the main points here today and flesh these out over the next few days for each of the bullet points.  
  
SQL Developer support several types of tuning activities.  These are:  
  

- Explain Plan/ Autotrace and Diff
- Monitoring SQL
- SQL Tuning Advisor
- PLSQL Hierarchical Profiler

For Refactoring, there are several options as well, and these grow with every release.

- Code Surrounding
- Procedure extraction
- Local variable renaming
- Obfuscation

Instrumentation is a way of finding out what an application is doing, who is using it, how its doing and and how long it has taken.  In order to look at this from a database application point of view, we can break application instrumentation into a number of key areas.

- Debugging
- Logging
- Runtime registration
- Metric Collection

Each of these key areas have specific tools and processes which should be implemented as part of your application development and we will get into those in the section on Instrumentation.
