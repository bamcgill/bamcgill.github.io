---
title: "SQLDev: How unshared worksheets should work!"
date: 2014-05-28 13:45:00 +0000
last_modified_at: 2014-05-28 13:45:26 +0000
tags:
  - worksheet
  - unshared
  - SQL Developer
---

Unshared worksheets are created to have a private connection to the database.  When that unshared worksheet is closed, the connection and session for it should disappear as well.

This graphic shows what should happen!

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgURunDbqpW3m93XZ8XQan9gP173rKZTS6xBQy8XqqImM2Rzz8F7hU0snMX-FbRC8Y96KSuDpcBVY0E9buLWSMNDR3pHuNnfd7aRA2qlbykP7JW3lW48czehxTVV3lRI0OB1uBSitWnS0c/s1600/testunshareclose.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgURunDbqpW3m93XZ8XQan9gP173rKZTS6xBQy8XqqImM2Rzz8F7hU0snMX-FbRC8Y96KSuDpcBVY0E9buLWSMNDR3pHuNnfd7aRA2qlbykP7JW3lW48czehxTVV3lRI0OB1uBSitWnS0c/s1600/testunshareclose.gif)
