---
title: "Clickable SQL*Plus Errors"
date: 2013-05-03 02:21:00 +0000
last_modified_at: 2013-05-03 02:21:40 +0000
tags:
  - worksheet
  - oracle
  - SQL*Plus
  - SQL Developer
---

Running lots of scripts in SQL\*Plus is nice when they are working correctly. But what about when they fail?  Its a pain to figure out what went wrong, unless you have a log file and even then, you have to hunt the errors down.  
  
Well, I've had enough of that.  Laziness has forced us to create clickable errors in the SQL Worksheet as part of SQL Developer.  
  
Heres a simple example.  Take 3 statements, one of which has an obvious error.  Hitting F5 runs the script and the errors now appear in the script output.  Notice that they are coloured blue at this point to show us that they are clickable.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEggNpqP7uGSTVtO16b3AiE6ZFXUsjpYNAoeDqmOroP1zFH99SoV7w3fCAJlnJwH5kgROyNj9ySdDGEBsuT9TfH7JUE6qg9I1oK9Kp7hhdgSsFlAAPKyLHebICYZFru_SUSu-txeCFFI0Y8/s1600/untitled2.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEggNpqP7uGSTVtO16b3AiE6ZFXUsjpYNAoeDqmOroP1zFH99SoV7w3fCAJlnJwH5kgROyNj9ySdDGEBsuT9TfH7JUE6qg9I1oK9Kp7hhdgSsFlAAPKyLHebICYZFru_SUSu-txeCFFI0Y8/s1600/untitled2.gif)

When you click on the error, you get taken to the point where you made the error in the worksheet.  In this case, line 3.  One of the things we wanted to do as much as possible when doing this was to keep tabs on the error should we change the file.  Above, I add a few lines and return to click on the error and it brings us to the right spot again. In this instance, line 5.

The same thing works in files.  If we have a problem in a nested file like @test/test.sql, the error is reported and we can click on it in the same way and be brought to the file at the appropriate line and column offset.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhl-f5j9ihQ_pMKWLdzGd1d-CEpZnBZ48BVlW1uZieQ1LS10zScfNlW-NhpOcU2_C3lFSr0z-pYIqAMQsXD6LsS2L-rVOhuZnGTBj7KRA3V9GBhuMEp_sQ56IvSS5d090mEd2QsjHw9BC0/s1600/file.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhl-f5j9ihQ_pMKWLdzGd1d-CEpZnBZ48BVlW1uZieQ1LS10zScfNlW-NhpOcU2_C3lFSr0z-pYIqAMQsXD6LsS2L-rVOhuZnGTBj7KRA3V9GBhuMEp_sQ56IvSS5d090mEd2QsjHw9BC0/s1600/file.gif)
