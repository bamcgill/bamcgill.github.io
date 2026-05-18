---
title: "SDSQL - Editing Anyone?"
date: 2014-12-12 18:05:00 +0000
last_modified_at: 2014-12-12 18:06:52 +0000
tags:
  - sqlplus
  - sdsql
  - command line
  - SQLDEVELOPER
---

Since we dropped our beta out of [SQLDeveloper 4.1](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/sqldev-41ea-2372780.html) and announced [SDSQL](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/sqldev-41ea-2372780.html), we've been busy getting some of the new things out to users.  We support SQL\*plus editing straight out of the box, but one thing that was always annoying was the time when you make a mistake and can't fix it to you have finished typing to go back and add a line like this.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVIbqUhJsBt_nJXrMYtwXQ-QchgGciz3q7CPjRwQmZFrIlIMp5vgQEfSKt8_V3s6cUu1kG1nQtzjSkLHe6mZ1sBTgToSsdhx-g9VXJxij2tOb4TR6ys1pfLjCV6VsgNMTvvSZd0ajMdS8/s1600/2014-12-12+17_42_03.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVIbqUhJsBt_nJXrMYtwXQ-QchgGciz3q7CPjRwQmZFrIlIMp5vgQEfSKt8_V3s6cUu1kG1nQtzjSkLHe6mZ1sBTgToSsdhx-g9VXJxij2tOb4TR6ys1pfLjCV6VsgNMTvvSZd0ajMdS8/s1600/2014-12-12+17_42_03.gif)

  
This was always the way as console editors didn't let you move around, the best you could hope for on the command line was a decent line editor and anything above was printed to the screen and not accessible unless through commands like you see here in the images about..   
  
Well, not any more.  In SDSQL we've taken a look at several things like history, aliases and colors and we've now added a separate multiline console editor which allows you to walk up and down your buffer and make all the changes you want before executing?  Sounds normal, right? So, thats what we did.  Have a look and tell us what you think.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXAhPmTcZRxrzwKTn8uEkuqeKBgTMYyzTnx2uxQMxgbtHo9z_PoMItl29YxoUv6lZRDMvgk6UIpiRARBGGSWJaUdC3v1RZHJnnESHcGEiBlB0ywIgJBmkBv7pB2glAIHfhkU3VsF4dg08/s1600/2014-12-12+18_01_04.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXAhPmTcZRxrzwKTn8uEkuqeKBgTMYyzTnx2uxQMxgbtHo9z_PoMItl29YxoUv6lZRDMvgk6UIpiRARBGGSWJaUdC3v1RZHJnnESHcGEiBlB0ywIgJBmkBv7pB2glAIHfhkU3VsF4dg08/s1600/2014-12-12+18_01_04.gif)
