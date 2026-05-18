---
title: "SQL*Plus Commands"
date: 2011-07-04 16:37:00 +0000
last_modified_at: 2011-07-04 16:48:23 +0000
tags:
  - SQL_Developer SQL*Plus
  - oracle
  - SQL*Plus
  - define
  - scan
  - substitution variables
---

Its funny how many people forget we support a lot of the basic SQLPlus functionality in SQL Developer. For example, today, [Paulo](http://apex-notes.blogspot.com/2007/09/i-use-substitution-string-in-my.html) blogged on how to stop scanning for substitution variables in a script.

He rightly pointed to the deprecated 'SET SCAN OFF' and the current 'SET DEFINE OFF' to fix his problem.

We support a lot of plus parameters in SQL\*Plus and are adding more on each release. For now, though, if you are using SQLDeveloper and are looking for the current settings in the worksheet, you can use the 'show all' command which shows the state of any parameters that are in force at that time.

e.g., The default will give you this.

appinfo is OFF and set to "SQL Developer"

arraysize default

autocommit OFF

autoprint OFF

autotrace OFF

copycommit 0

define "&"

echo OFF

escape OFF

FEEDBACK ON for 6 or more rows

null ""

serveroutput OFF

spool OFF

sqlcode 0

termout ON

timing OFF

USER is HR

verify ON

For supported SQL\*Plus commands you can also use 'help' command which lists the commands supported. e.g.,

For help on a topic type help

List of Help topics available:

/

@

@@

ACCEPT

APPEND

ARCHIVE LOG

CHANGE

COLUMN

CONNECT

COPY

DEFINE

DEL

DESCRIBE

DISCONNECT

EDIT

EXECUTE

EXIT

GET

HOST

INPUT

LIST

PASSWORD

PAUSE

PRINT

PROMPT

QUIT

REMARK

RESERVED WORDS

RUN

SAVE

SET

SHOW

SHUTDOWN

SPOOL

SQLPLUS

START

STARTUP

TIMING

UNDEFINE

VARIABLE

WHENEVER OSERROR

WHENEVER SQLERROR

XQUERY

I'll follow this up with another post of the SQLDeveloper 3.1 functionality where we are supporting more of the printing functionality around column formatting and titles.
