---
title: "Multi Tasking - Men can't do it."
date: 2008-09-02 13:34:00 +0000
last_modified_at: 2008-09-02 13:49:43 +0000
tags:
  - Threads
  - Openworld
  - SQLDEVELOPER ORACLE
  - Migration
---

But SQL Developer can. We've spent some time reworking the worksheet for 2.0 to allow several things to happen.  

1. Allow you to register pre and post statement listeners so you can do things with the code before and after it is run.
2. Added a tasking framework which handles background tasks to allow the users more immediate control, response and information as they use the tool.

The listeners are being integrated into the worksheet and the tasking framework is being used in several places already for 2.0. The navigator is making use of it as will most things wh[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj7EVb6ueube49_bCTT9DIeTbGsfAc3qKfBNiI7WEBc0pVnW5CKyXV0LGcwL7UpiGPhxvJUv2AHMRSMEbMUl_7wdb3PgYlX4JCPlLzk9dQjbfJwW6vUNsX4YeLXQhYhgAvmXwa1Ts8iacU/s200/taskbar.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj7EVb6ueube49_bCTT9DIeTbGsfAc3qKfBNiI7WEBc0pVnW5CKyXV0LGcwL7UpiGPhxvJUv2AHMRSMEbMUl_7wdb3PgYlX4JCPlLzk9dQjbfJwW6vUNsX4YeLXQhYhgAvmXwa1Ts8iacU/s1600-h/taskbar.PNG)ich take more than a few seconds to complete.  
On the bottom of the tool, we have a 'knight Rider' bar showing the task running.  
We house these tasks in another dockable window which shows the tasks and allows the user to configure and manage them through out their life before they disappear when the task is complete and the threaded task they represent is gone.[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi56tDmGspa3TeQBDZAl092rgVcUcaWOaGVJBubP4HPZCCr5E4eUtiB4h6UJjxmYNH1_9Y9HSsV027XvTahbJfWmmCXzrj1X6HtqJKl3pnpsfOyQPvm76vRk6AkgwL9owUoS8VGpFI-XFA/s200/tasks.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi56tDmGspa3TeQBDZAl092rgVcUcaWOaGVJBubP4HPZCCr5E4eUtiB4h6UJjxmYNH1_9Y9HSsV027XvTahbJfWmmCXzrj1X6HtqJKl3pnpsfOyQPvm76vRk6AkgwL9owUoS8VGpFI-XFA/s1600-h/tasks.PNG)All of these things, we'll be showing at Open World from the 15th of September so if you're going drop along to a session on base SQL Developer stuff or some of the other Migration or modeling sessions. You can see whats going on [here](http://www28.cplan.com/cc208/catalog.jsp?ilc=208-1&ilg=english&isort_sessions=&isort_demos=&isort_exhibitors=&is=yes&ip=%3C%2Fipresentations%3E&isort_sessions_type=&isort_exhibitors_type=&isort_demos_type=&search_sessions=yes&search_exhibitors=yes&icriteria1=+&icriteria2=+&icriteria5=+&icriteria8=Oracle&icriteria9=+&icriteria6=&icriteria3=+&icriteria7=SQL+Developer).
