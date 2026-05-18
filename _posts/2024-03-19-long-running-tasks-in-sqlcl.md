---
title: "Long Running Tasks in SQLcl"
date: 2024-03-19
last_modified_at: 2026-05-18
tags:
  - SQLcl
  - Oracle
  - Database Tools
  - Liquibase
excerpt: "SQLcl 24.1 introduced background task execution — run any command in parallel, name it, track it, and wait for it to finish."
---

SQLcl 24.1 introduced a way to run tasks in parallel. Any command that makes sense to run in the background — a long-running query, a Liquibase changeset generation, a data export — can now be kicked off without blocking your session.

Three commands work together to make this happen: `background`, `jobs`, and `wait4`.

## The commands

**`background`** (or `bg`) takes any SQLcl or SQL*Plus command and runs it as a background task. You can name the task and optionally wait for another task to complete before it starts.

```
SQL> help background syntax
 background|bg [-wait4|-w4 <wait4>] [-taskname|-tn <taskname>] <commandspec>
```

**`jobs`** lists and manages background tasks — check status, view logs, or clean up finished work.

**`wait4`** pauses execution until a specific task (or list of tasks) completes, or waits for a given number of milliseconds. Useful for scripting dependencies between tasks.

## Running a command in the background

Take a Liquibase changeset generation as an example. Normally you'd run it in the foreground:

```
SQL> liquibase generate-db-object -object-name employees -object-type table -sql
--Starting Liquibase at 2024-03-19T23:10:47 (version 4.26.0)
Changelog created and written out to file employees_table.xml
Operation completed successfully.
```

That blocks your session until it finishes. With `background`, you can fire it off and keep working:

```
SQL> background -taskname lb-employees liquibase generate-db-object -object-name employees -object-type table -sql
Started task with id: 2

SQL> jobs
 2: [ Running ] lb-employees (/Users/bamcgill/.sqlcl/jobslogs/lbemployees.log)
```

The task runs in the background. Check on it with `jobs`, and pull the output with `jobs logs`:

```
SQL> jobs logs -id 2
--Starting Liquibase at 2024-03-19T23:21:09 (version 4.26.0)
Changelog created and written out to file employees_table.xml
Operation completed successfully.

SQL> jobs
 2: [ Finished ] lb-employees (/Users/bamcgill/.sqlcl/jobslogs/lbemployees.log)
```

The output is identical to running the command in the foreground — it's just not blocking you while it works.

## Where this matters

The obvious use case is kicking off several independent tasks at once — generate changesets for multiple schemas, run exports in parallel, or execute long-running reports while you continue working in the same session.

Combined with `wait4`, you can script task dependencies: start task A and task B in parallel, then `wait4` both before starting task C. That's a simple but effective orchestration pattern without leaving the command line.

[Download the latest SQLcl from oracle.com](https://www.oracle.com/database/sqldeveloper/technologies/sqlcl/download/) and give it a try.
