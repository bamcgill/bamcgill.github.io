---
title: "Explain Plan, Autotrace and Diff"
date: 2011-12-05 18:42:00 +0000
last_modified_at: 2011-12-05 18:44:53 +0000
tags:
  - autotrace
  - explain plan
  - Tuning
  - SQLDEVELOPER
---

A SQL statement can be executed in many different ways, such as full table scans, index scans, nested loops, and hash joins. The query optimizer determines the most efficient way to execute a SQL statement after considering many factors related to the objects referenced and the conditions specified in the query. This determination is an important step in the processing of any SQL statement and can greatly affect execution time.  
  
  

The `EXPLAIN` `PLAN` results let you determine whether the optimizer selects a particular execution plan, such as, nested loops join. It also helps you to understand the optimizer decisions, such as why the optimizer chose a nested loops join instead of a hash join, and lets you understand the performance of a query.

  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg4aCjTT5WnjGhmT93B1_kj4yt7HFBqaJ_QGX9zDSk3DvnpdJLs8Wbvmy7vDjwxtxk9pVw7kp2rGlv748bUFzxodfUuh1j5EC8cLY1SlJCxXtz1NpRPIiJTnVSEYaYFl8zgS1JewGybdmw/s320/explain.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg4aCjTT5WnjGhmT93B1_kj4yt7HFBqaJ_QGX9zDSk3DvnpdJLs8Wbvmy7vDjwxtxk9pVw7kp2rGlv748bUFzxodfUuh1j5EC8cLY1SlJCxXtz1NpRPIiJTnVSEYaYFl8zgS1JewGybdmw/s1600/explain.PNG)

  
You can examine the execution plan chosen by the optimizer for a SQL statement by using the EXPLAIN PLAN button on the worksheet. When the statement is issued, the optimizer chooses an execution plan and then inserts data describing the plan into a database table. SQL Developer looks at the table and displays the tree operations.  Looking at the example, we can see the query is doing a Cartesian product  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgnjZXAqHX2YTCCcELv3Uw_AaBakJRNBNYJHMghP-L7TUwGdriXhuDDVXt18CfOZS3RQI50Dg0086aqqPdX_5u7qlzpBKNbU7YFZSYzF4rF9NVsvRQuRanx6cd4ut_-JeS14lb_k98x39w/s320/autotrace.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgnjZXAqHX2YTCCcELv3Uw_AaBakJRNBNYJHMghP-L7TUwGdriXhuDDVXt18CfOZS3RQI50Dg0086aqqPdX_5u7qlzpBKNbU7YFZSYzF4rF9NVsvRQuRanx6cd4ut_-JeS14lb_k98x39w/s1600/autotrace.PNG)

Similary, when you use autotrace, which, on SQL Developer, is the button beside the explain plan. AND, you can diff two plans to  see what the difference is between two plans, as you can see below.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2ThljDskC6N7ebtgYZMbrnMWGAWzPvnXp6fUTYvYseUhVj_wocO1d-hX16-o7eLu3NtvcyCVkd3mf-KklPgx2z9N2bvOMbgF_l1TD_44Nx5hC0srWKiq42Omiw3XqxCrG2hR2XjJIqCw/s400/explain_trace_diff.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2ThljDskC6N7ebtgYZMbrnMWGAWzPvnXp6fUTYvYseUhVj_wocO1d-hX16-o7eLu3NtvcyCVkd3mf-KklPgx2z9N2bvOMbgF_l1TD_44Nx5hC0srWKiq42Omiw3XqxCrG2hR2XjJIqCw/s1600/explain_trace_diff.PNG)

  
However, even though we can show you what a plan looks like, it cannot differentiate between well-tuned statements and those that perform poorly.  
  
  
  

For example, an `EXPLAIN` `PLAN` output that shows that a statement uses an index does not necessarily mean that the statement runs efficiently. Sometimes indexes can be extremely inefficient. In this case, you should examine the following:

- The columns of the index being used
- Their selectivity (fraction of table being accessed)

It is best to use `EXPLAIN` `PLAN` to determine an access plan, and then later prove that it is the optimal plan through testing. When evaluating a plan, examine the statement's actual resource consumption.

And from the doc!:

In addition to running the `EXPLAIN` `PLAN` command and displaying the plan, you can use the `V$SQL_PLAN` views to display the execution plan of a SQL statement. After the statement has executed, you can display the plan by querying the `V$SQL_PLAN` view. `V$SQL_PLAN` contains the execution plan for every statement stored in the cursor cache.

The `V$SQL_PLAN_STATISTICS` view provides the actual execution statistics for every operation in the plan, such as the number of output rows and elapsed time. All statistics, except the number of output rows, are cumulative. For example, the statistics for a join operation also includes the statistics for its two inputs. The statistics in `V$SQL_PLAN_STATISTICS` are available for cursors that have been compiled with the `STATISTICS_LEVEL` initialization parameter set to`ALL`.

The `V$SQL_PLAN_STATISTICS_ALL` view enables side by side comparisons of the estimates that the optimizer provides for the number of rows and elapsed time. This view combines both `V$SQL_PLAN` and `V$SQL_PLAN_STATISTICS` information for every cursor.

Anyway, don't take my word for all this, try it on SQLDeveloper today and you can follow Tom Kyte's process for tuning sql statements.  

<http://asktom.oracle.com/pls/asktom/f?p=100:11:0::::P11_QUESTION_ID:8764517459743>
