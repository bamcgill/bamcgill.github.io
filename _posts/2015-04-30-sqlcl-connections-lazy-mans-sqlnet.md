---
title: "SQLcl connections - Lazy mans SQL*Net completion"
date: 2015-04-30 16:30:00 +0000
last_modified_at: 2015-04-30 16:30:32 +0000
tags:
  - sqlplus
  - sqlcl
  - command line
  - SQLDEVELOPER
---

Turloch posted [this](http://totierne.blogspot.in/2015/04/net-command-persistently-store-network.html) today, which is like aliases for SQL\*Net connection URL's which are used to connections like this:  
  

```
connect <USERNAME>/<Password>@URL
```

  
This works great and you can simplify your connection strings that you use.  Vadim wired this into the code completion and we can now code complete via  key, a connection string that you have used before or you can set up a new now using the net command.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6NFd8Ze17uyMIRBsIhvM5ukRKUi2qhHbF3-KaaiBh_AXqoasDUoZOnRCs9szTPuOzkpdbkg9VQ6bSuu6_6dyiPaLpy-DyAQyLUpkzew0NWFSu7D7NGO7Alh8s_Vwl36CF_2yuHAtRwBg/s1600/2015-04-30+17_17_16.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6NFd8Ze17uyMIRBsIhvM5ukRKUi2qhHbF3-KaaiBh_AXqoasDUoZOnRCs9szTPuOzkpdbkg9VQ6bSuu6_6dyiPaLpy-DyAQyLUpkzew0NWFSu7D7NGO7Alh8s_Vwl36CF_2yuHAtRwBg/s1600/2015-04-30+17_17_16.gif)
