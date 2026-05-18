---
title: "Clicking around the worksheet"
date: 2011-01-14 11:33:00 +0000
last_modified_at: 2011-01-14 12:19:09 +0000
tags:
  - SQLDEVELOPER ORACLE
  - worksheet
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhgMpxNtFa-knxuVMqaIHfuoYhq582nq0pv5LQyC9EG5DBew5xXXciVuMvzaHZoUIsxx9vbDzcq1P1iO4d14uMcOcREgFWrrm5va2bhLXs7RIBZuArNLF_AcwOoj576QNcRMPmysEhs5DE/s200/ctrl-click-2.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhgMpxNtFa-knxuVMqaIHfuoYhq582nq0pv5LQyC9EG5DBew5xXXciVuMvzaHZoUIsxx9vbDzcq1P1iO4d14uMcOcREgFWrrm5va2bhLXs7RIBZuArNLF_AcwOoj576QNcRMPmysEhs5DE/s1600/ctrl-click-2.PNG)As we have been getting close to another EA release, one thing which struck me as pretty cool and something we haven't talked about in a while are the click actions in the worksheet.

Looking at the image on the right, we can see the first action that is available. By holding the  down while we move the mouse over the table employees we can see that it is highlighted and underlined. If we click on this, it will open up the appropriate editor.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj47HKcY642-_qytE_T-XsKE7NmFo1VgNA9ZsjvHgTeYPPjmwzOvL6yN4L5eUoD9426xhy9GT6P72cDzvQxlr2Bix8CsQb0yFoELkFJNW4SJMkeNk6N5JoT35D0cGyhfVNA8Pn9gd17WN4/s200/ctrl-click-3.PNG)

Next we can see the list of SQL\*Plus files below the query in the worksheet. Normally, these are written by locating the file and putting the appropriate syntax in place.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZvWR76wgR6BxY7Uoyyw5-55WO5AyChSdEmoOJi1wLIeSTaOnj6UBtDKIdJEj6PaN8W9ubpuE3veoWnYH1w5BsVqfayWiGq2fGLDJJgA5CsgVS9Q9USNKc-57_F2uSvl3dE1qeyvJDgJU/s200/ctrl-click-4.PNG)

Well to make reviewing this files easier, we've added a similar functionality to these files. This way when we click on a file call, and the file exists, we can open that in an editor for reviewing and editing.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXfH0ZiINYNglY0luen9boCUCQTcN5EB59SLWaa-JFULIBt1Orv_sL-z4Cboem9QH-EdkwvwUmZ-El5_4Pz9ElHGKKV8BgLqf2C3i56yzB8dJpmVEI1Ft3A-qeAXHmFdI-vTXT6kwLAr4/s200/ctrl-click-5.PNG)

There are three places where we will look for files. The first is straight forward and is the complete file path name.

@/MY/FULL/PATH/NAME/BARRY.SQL

The second is taking files in your ORACLE\_HOME directory and the '?' directive denotes that directory. so a typical directory looks like this.

@?/admin/catalog.sql

Finally, the last one, has the format:

@barry.sql

This last file structure takes the file from the USER\_HOME directory in SQL Developer or, the place where you ran a script, or if you have the script directory set in the worksheet preferences, it will look there.

This will be available in our next EA, EA3.

Enjoy!
