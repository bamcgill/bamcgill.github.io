---
title: "Detecting Hangs in Java"
date: 2011-01-17 12:08:00 +0000
last_modified_at: 2011-01-17 13:53:36 +0000
tags:
  - Java
  - stack
  - SQL Developer
---

One of the things we are looking into right now is performance in SQL Developer and concurrency of operations. Sometimes, operations that are spawned on the [EDT](http://en.wikipedia.org/wiki/Event_dispatching_thread) should not be there.

These are typical scenarios of the [SwingUtilities.invokelater(Runnable)](http://download.oracle.com/javase/6/docs/api/javax/swing/SwingUtilities.html#invokeLater(java.lang.Runnable)).

These operations show themselves to the user as a perceived hang in the UI which is not wanted.

There are two ways to find these in Java.

1. You can use [JStack](http://download.oracle.com/javase/1.5.0/docs/tooldocs/share/jstack.html), which is part of the Java SDK. This is very simple to run, giving it the Process ID of the java program and it prints a stack dump of the JVM.  
     
   Here is some example output from a recent one I found with it.  
     
   "AWT-EventQueue-0" prio=6 tid=0x041ac800 nid=0x10f0 runnable [0x0398b000]  
    java.lang.Thread.State: RUNNABLE   
   at java.util.regex.Pattern$BnM.optimize(Pattern.java:4946)  
   at java.util.regex.Pattern.compile(Pattern.java:1473)   
   at java.util.regex.Pattern.(Pattern.java:1133)  
   at java.util.regex.Pattern.compile(Pattern.java:823)  
   at oracle.dbtools.migration.parser.ext.ExtAutoIndentWriter.  
    (ExtAutoIndentWriter.java:30)  
     
   This is the relevant snippet of the trace which shows that we are running on the event queue. Fixing this is a simple case of moving it out of this thread to one of its own, in this case, we've created a RaptorTask to take care of it.
2. The other way to find these could be to build in a log handler to your application which can pop a stack trace when a hang is detected. In SQL Developer, we have log handlers like this built in and when the appropriate flag is set, and the EDT is waiting for a predetermined amount of time, we pop a stack trace, right there to show what was running at that point in time.

As we go through these, its making SQL Developer much more performant and responsive working with remote databases and allowing the user to keep control of the UI.
