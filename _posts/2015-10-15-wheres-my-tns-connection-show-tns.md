---
title: "Wheres my TNS connection?  SHOW TNS"
date: 2015-10-15 09:19:00 +0000
last_modified_at: 2015-10-15 09:22:23 +0000
tags:
  - Connections
  - tnsnames
  - SQLDEVELOPER
  - tns
  - TNS_ADMIN
  - sqlcl
---

Lots of users have been head scratching as to which tnsnames.ora is being found and used when  connecting to the database with SQLDeveloper and with SQLcl.  
  
In the latest release we've added another new command.  
  

**SHOW TNS**

  
What this will do is walk the locations where we look for tnsnames.ora and list these out in order.  Then it will tell you which one the tool will actually use and list the entries for you.  
  
So, with nothing set, no ORACLE\_HOME, no TNS\_ADMIN, here's what you get.  TNS is going to look in your home directory for a file called tnsnames.ora or .tnsnames.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEguFtwDffp4DvRBmPKBbLnDK177_bpwN0w41edQfoIvWnsxWMYAxGswYLTzolCgISMvBJ8xBgkud4fkMZqYh0P3hD3PcAPqKxSgBhpJtHRsnp9peukunFuHbtX-8jnsMkNpff-PijWC7vU/s400/Screen+Shot+2015-10-15+at+09.35.20.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEguFtwDffp4DvRBmPKBbLnDK177_bpwN0w41edQfoIvWnsxWMYAxGswYLTzolCgISMvBJ8xBgkud4fkMZqYh0P3hD3PcAPqKxSgBhpJtHRsnp9peukunFuHbtX-8jnsMkNpff-PijWC7vU/s1600/Screen+Shot+2015-10-15+at+09.35.20.png)

  
Now, if we have an ORACLE\_HOME set, we'll look for $ORACLE\_HOME/network/admin/tnsnames.ora  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjh6Jqs8pE-LrgJEtj-mAznEVfTl6fnT33p6T24_cZYyigMKBCVQHbswHuBv9Ig3GiVbfUqque1a4ByiBYKZARCaO2jKXf6bbkTZGajtLI7SDtZY_tpdtv4hBua5CT2A1iMgtOMna9MAAQ/s400/Screen+Shot+2015-10-15+at+09.37.53.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjh6Jqs8pE-LrgJEtj-mAznEVfTl6fnT33p6T24_cZYyigMKBCVQHbswHuBv9Ig3GiVbfUqque1a4ByiBYKZARCaO2jKXf6bbkTZGajtLI7SDtZY_tpdtv4hBua5CT2A1iMgtOMna9MAAQ/s1600/Screen+Shot+2015-10-15+at+09.37.53.png)

  
Further, if we set TNS\_ADMIN, it will override ORACLE\_HOME and go to that location as shown here.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3CdYFG_bgWqpZLg9BNMkaBa0Xg8j9ZNweAhU7fbEZC5Zb-AkhqeoRrCvDhhz7qLsB3f6tyG_i3c0UbhlFV7r3iUkLRx-vGFslumQDdxqmJWJklBOhrCmF-wmvYJCTkMYKg_dB9kd1JbM/s400/Screen+Shot+2015-10-15+at+09.42.57.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3CdYFG_bgWqpZLg9BNMkaBa0Xg8j9ZNweAhU7fbEZC5Zb-AkhqeoRrCvDhhz7qLsB3f6tyG_i3c0UbhlFV7r3iUkLRx-vGFslumQDdxqmJWJklBOhrCmF-wmvYJCTkMYKg_dB9kd1JbM/s1600/Screen+Shot+2015-10-15+at+09.42.57.png)

  
Lastly, we'll come back to the User directory. If you have a tnsnames.ora there or a .tnsnames, it will override everything and this is what will be used.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhoZiR9-6HDeZyFbKzan0MItPuhDy8XHx6d06d4kpmqU0J7DCGn6Ekgsfsvz0t76R-k7TwCnKCdb25ECfgAnOEaOyxwUwVHrRZZ8aIrFcXXiXhjOAIDF_hh8f5Ue7uAOP3Fgx0oXmfHBA0/s400/Screen+Shot+2015-10-15+at+09.47.28.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhoZiR9-6HDeZyFbKzan0MItPuhDy8XHx6d06d4kpmqU0J7DCGn6Ekgsfsvz0t76R-k7TwCnKCdb25ECfgAnOEaOyxwUwVHrRZZ8aIrFcXXiXhjOAIDF_hh8f5Ue7uAOP3Fgx0oXmfHBA0/s1600/Screen+Shot+2015-10-15+at+09.47.28.png)

  
  
Now, go ahead and make a connection.  You can then do another new command called  
  

**SHOW CONNECTION**

  
which will show you how you are connected and what you are connected to.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh7_yRRHORZPQ-YJzw6efpTVlmQ69PIKqWiOesdjPTO4eeRYjUSyn5W8JnbvuXppvHX_iezIp9b7nhcUpr7F0pypHjRsi0h1YQpuu0yQfIqJKnYOdqB5XfkYa1KL09GQp4VCF9dkmjKy4U/s640/2015-10-15+10_09_06.gif)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh7_yRRHORZPQ-YJzw6efpTVlmQ69PIKqWiOesdjPTO4eeRYjUSyn5W8JnbvuXppvHX_iezIp9b7nhcUpr7F0pypHjRsi0h1YQpuu0yQfIqJKnYOdqB5XfkYa1KL09GQp4VCF9dkmjKy4U/s1600/2015-10-15+10_09_06.gif)

  
Finally, you can get a look at which driver you are using for a connection using  
  

**SHOW JDBC**

  
which will show something like this, detailing types, versions and the URL of the connection you have.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQz7g-1xx4QzVD5-tGe7fGACPJBS88whr1oCwCTPO2sj0fXv8rFF3JMi3lgM1dbfCP6t16R16OVOW6FWvTwT5WNLLMiPHjInYeusemClyE-xroHINtLuf_WmeuHZHiZN6ZuscvH3IEmII/s400/Screen+Shot+2015-10-15+at+10.14.13.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQz7g-1xx4QzVD5-tGe7fGACPJBS88whr1oCwCTPO2sj0fXv8rFF3JMi3lgM1dbfCP6t16R16OVOW6FWvTwT5WNLLMiPHjInYeusemClyE-xroHINtLuf_WmeuHZHiZN6ZuscvH3IEmII/s1600/Screen+Shot+2015-10-15+at+10.14.13.png)
