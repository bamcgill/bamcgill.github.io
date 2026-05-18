---
title: "SQLcl - Code editing on the console"
date: 2015-05-01 18:08:00 +0000
last_modified_at: 2015-05-01 18:08:17 +0000
tags:
  - editor
  - oracle
  - cool
  - command line
  - SQLDEVELOPER
  - sqlplus
  - sqlcl
---

We've been playing with our console drawing in SQLcl for a while now and this week, we hooked up some keys to make editing and running much easier.  The video will show the following keys for managing your buffer in the console.  This will make it into the next Early Access candidate soon.  
  

- **up arrow** - previous history (this will continue to show you the next history unless you move into the text to edit it.
- **down arrow** - next history which is the same as above.

If we are editing and not showing history, then the up and down arrow will move up and down the buffer.

- **ctrl-W** will take you to the top left of the buffer and **ctrl-S** will take you to the bottom of the buffer.
- left arrow moves right, with **ctrl-A** taking you to extreme left of that line
- **right arrow** moves right and **ctrl-E** takes you to the extreme right of that line
- **ESC** takes you out of edit mode, back to the SQL> prompt
- **ctrl-R** will execute your buffer if you are editing it.

|  |
| --- |
|  |
|  |

Editing SQL in SQLcl

At the start of the video, we paste in a large piece of SQL from [Kris' blog](http://krisrice.blogspot.co.uk/2015/04/repeating-another-sqlcl-ea-release.html) and all NBSP get stripped out so you get the full SQL and none of the dross.

If you are at the end of the buffer and terminate your statement correctly, the next **CR** will run the contents of your buffer.  If you are anywhere else in the buffer, **ctrl-R** will run the buffer for you.

Check out the latest one on OTN and come back for these features when we drop the new version of SQLcl on OTN.
