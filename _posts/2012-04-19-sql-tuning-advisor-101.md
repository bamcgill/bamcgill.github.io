---
title: "SQL Tuning Advisor - 101"
date: 2012-04-19 07:53:00 +0000
last_modified_at: 2012-04-19 07:53:02 +0000
tags:
  - worksheet
  - sql tuning advisor
  - SQLDEVELOPER
---

The DBMS\_SQLTUNE package is the interface for tuning SQL on demand. Its Doc pages are [here](http://docs.oracle.com/cd/E11882_01/appdev.112/e25788/d_sqltun.htm).  Have a look.  There is a lot of stuff to do to set a tuning task, run it, report on it and then get it to do something useful.  We've wrapped all that into our SQL Tuning Advisor function which means you dont need to start writing plsql API calls to make this work.  Stick in your dodgy query, click the advisor button and visualize the results.   
  
Here's a look at how to do this.  Firstly, we need to grant a few permissions to our user. I'm doing this as sys.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgbkHlyvbt64qtPYgvF_icXxzIXMeTkrFhlnH7cjXN2qc3FAdoyd5njLH1tE2zatBni1NN4QEizI1omEbLCEzuEyxqQgceOqwcKQq6yg-wz4bFq3sP8D9Wi4naMIDsNco5v6UcxsyXiZTc/s320/Screen+Shot+2012-04-19+at+10.24.11.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgbkHlyvbt64qtPYgvF_icXxzIXMeTkrFhlnH7cjXN2qc3FAdoyd5njLH1tE2zatBni1NN4QEizI1omEbLCEzuEyxqQgceOqwcKQq6yg-wz4bFq3sP8D9Wi4naMIDsNco5v6UcxsyXiZTc/s1600/Screen+Shot+2012-04-19+at+10.24.11.png)

 Then, for this demo, I want to clean out all the statistics on the tables I want to look at.   

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgAqWDJMu8k2iOMTIa_Uw4ARw7J-Wl4R_TpqLqh7Ua2YHOUNq9b6v3MXpEDDdZTFEQwcHpkE7pDb5m_-l-ojAlJxQEM7xRHWFFCQucMNFJe6VEKMB21fdF8lnmBwAnszPVLQ989xniwnng/s320/Screen+Shot+2012-04-19+at+10.25.31.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgAqWDJMu8k2iOMTIa_Uw4ARw7J-Wl4R_TpqLqh7Ua2YHOUNq9b6v3MXpEDDdZTFEQwcHpkE7pDb5m_-l-ojAlJxQEM7xRHWFFCQucMNFJe6VEKMB21fdF8lnmBwAnszPVLQ989xniwnng/s1600/Screen+Shot+2012-04-19+at+10.25.31.png)

 Now, here's my initial query, getting total and mean salary grouped by departments.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhuhKLD4hUAiBtuIUDgj_b0UB2LfaUg4Luwcr0ONU7yta4T_cEz_rzG6uleg-p44tRB_sq-I57SXa6jKAQi4qUsqRqdhCZbQoALBItFiMGMyImSFRwMir6rud5hv1YsAcggirCGixOf-lk/s1600/Screen+Shot+2012-04-19+at+10.26.21.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhuhKLD4hUAiBtuIUDgj_b0UB2LfaUg4Luwcr0ONU7yta4T_cEz_rzG6uleg-p44tRB_sq-I57SXa6jKAQi4qUsqRqdhCZbQoALBItFiMGMyImSFRwMir6rud5hv1YsAcggirCGixOf-lk/s1600/Screen+Shot+2012-04-19+at+10.26.21.png)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgJ9h3Fy7zZwAR9Aa36IB6hj7XbGT9UxNLwvfMbS0YeS5Z-da9FuOKlbCAruAyq2ojn9qT_Fv0SG3a1w1PgNabNrRlRM1i5rKKxfzVdsJmdJVLJSnEnx_gjl9p0Pzy6PMBshVTzMsFgF8U/s1600/ss+now.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgJ9h3Fy7zZwAR9Aa36IB6hj7XbGT9UxNLwvfMbS0YeS5Z-da9FuOKlbCAruAyq2ojn9qT_Fv0SG3a1w1PgNabNrRlRM1i5rKKxfzVdsJmdJVLJSnEnx_gjl9p0Pzy6PMBshVTzMsFgF8U/s1600/ss+now.png)

When we then run the tuning advisor, a new tab appears on the worksheet which has the main results from the tuning sesstion.  This tab has four main sections to it. These are the statistics which the advior found on the objects in the query, changes to the profile which is in use, any indexes which need to be added.  Finally, if needed, there is a restructuring tab which may have some sql to help you restructure your query.  
  
  

Finally, on the right hand side, we can see the details of tuning job.  The SQL\_TUNE package generate text which we organise into the tabs.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirtNFg4KvphAi2rDreBl8A0re-oGblkdx8oI8UTguyJlxc9hazH6XQ_TPNX2ZeTSaOyZGXqim4xcA001G6TYimMU2hjZGA-ZbfWpfBCvEPQ6A4Zoqhw4FusF097RQXMXqbAKJ9_MknldM/s320/Screen+Shot+2012-04-19+at+10.28.16.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirtNFg4KvphAi2rDreBl8A0re-oGblkdx8oI8UTguyJlxc9hazH6XQ_TPNX2ZeTSaOyZGXqim4xcA001G6TYimMU2hjZGA-ZbfWpfBCvEPQ6A4Zoqhw4FusF097RQXMXqbAKJ9_MknldM/s1600/Screen+Shot+2012-04-19+at+10.28.16.png)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgp98_esHMxEU-RjufrmQIZ-Y_rrddyR9u2GS8s9iYn0DFQxZFwLIBTxnWMXODEPQMjHZDdjm230-LUanfLTYwfOhxRJ7W3_Oq-dttqPqXerclHEt4GSIhAlgeAJ4ZLPVffFIdrwl2pg0U/s400/Screen+Shot+2012-04-19+at+10.32.15.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgp98_esHMxEU-RjufrmQIZ-Y_rrddyR9u2GS8s9iYn0DFQxZFwLIBTxnWMXODEPQMjHZDdjm230-LUanfLTYwfOhxRJ7W3_Oq-dttqPqXerclHEt4GSIhAlgeAJ4ZLPVffFIdrwl2pg0U/s1600/Screen+Shot+2012-04-19+at+10.32.15.png)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEghvAXXA9q7bicZ0-ly4KLMexxHUd1dNw4gcmdgfQ6qfzvlHq_2iaaxMW_Hw-B34HhHdGpqednCJAytS1UCzBA6IRLy8InjyqCSTEwbub74nmuTIkjW55CsiUDmskVo1zObMzbq4YXRKhA/s1600/Screen+Shot+2012-04-19+at+10.32.30.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEghvAXXA9q7bicZ0-ly4KLMexxHUd1dNw4gcmdgfQ6qfzvlHq_2iaaxMW_Hw-B34HhHdGpqednCJAytS1UCzBA6IRLy8InjyqCSTEwbub74nmuTIkjW55CsiUDmskVo1zObMzbq4YXRKhA/s1600/Screen+Shot+2012-04-19+at+10.32.30.png)

We can see from the output above that the statistics are not available and the tool is recommending refreshing statistics on the objects in the original query.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9RcB5-p9f96_jdFcRzy4uQGHdwzZP-PO21sDugvDn5ZReJb8KkFeFwDGpODMZm7HYSrEv68aIAtQp18S9MsCQwO1511tmFsE9nMgzG9tfkGjFQgTUKlN89qbtfPvw5dd2TY75hKdP-js/s320/Screen+Shot+2012-04-19+at+10.29.36.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9RcB5-p9f96_jdFcRzy4uQGHdwzZP-PO21sDugvDn5ZReJb8KkFeFwDGpODMZm7HYSrEv68aIAtQp18S9MsCQwO1511tmFsE9nMgzG9tfkGjFQgTUKlN89qbtfPvw5dd2TY75hKdP-js/s1600/Screen+Shot+2012-04-19+at+10.29.36.png)

  
We can then go and analyze the tables to see if that helps.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFsJQXBbz6Yl1CUnBjqckrbzRmO5WwI_E55P8YPqnzwialKXeThcde-qWu0-_-aarLXni9zZmgjjBaSLdBXbnpeGscwqW-X_U8pypg_FP2OK5pcgxs0xTAq55aR1yPpJUbusn44ogz0Ww/s320/Screen+Shot+2012-04-19+at+10.29.47.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFsJQXBbz6Yl1CUnBjqckrbzRmO5WwI_E55P8YPqnzwialKXeThcde-qWu0-_-aarLXni9zZmgjjBaSLdBXbnpeGscwqW-X_U8pypg_FP2OK5pcgxs0xTAq55aR1yPpJUbusn44ogz0Ww/s1600/Screen+Shot+2012-04-19+at+10.29.47.png)

  
We can then check that the stats are fresh and at the time of posting, this is current.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhjSLcwixkZMK6PC4bTTurzdyuaMrd7_VEqyQiFN4jt3Bej0pneLG-4Eh8qRbxzhpSLwK3PNhiRtHF6A7wyNzy7nbtslGkIT3HuIMR7m2ce3je1w2xbE2kUMjoZ7yXp_qVJGdFvLlKj-tM/s1600/Screen+Shot+2012-04-19+at+10.31.27.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhjSLcwixkZMK6PC4bTTurzdyuaMrd7_VEqyQiFN4jt3Bej0pneLG-4Eh8qRbxzhpSLwK3PNhiRtHF6A7wyNzy7nbtslGkIT3HuIMR7m2ce3je1w2xbE2kUMjoZ7yXp_qVJGdFvLlKj-tM/s1600/Screen+Shot+2012-04-19+at+10.31.27.png)

  
  
Now, going back the tuning advisor and running it again, shows some different stats  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgmMrvg7ntSdKBoKI_WVEFH1qjrURWS4Y7fuNDrkQLOnwKpvrLqKWOJ9fsowowswF1BdpT0myGZLaxhFMiJ2cyWSgGvekrHj1wrCP7reL11ot0yFKOb5O_jMNG1lt16KvY5hsraZKfpirs/s320/Screen+Shot+2012-04-19+at+10.33.28.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgmMrvg7ntSdKBoKI_WVEFH1qjrURWS4Y7fuNDrkQLOnwKpvrLqKWOJ9fsowowswF1BdpT0myGZLaxhFMiJ2cyWSgGvekrHj1wrCP7reL11ot0yFKOb5O_jMNG1lt16KvY5hsraZKfpirs/s1600/Screen+Shot+2012-04-19+at+10.33.28.png)

  
Heres the final look at what the Tuning advisor tells us at the end of the second run.  This is the standard text output that comes from the tuning package  
  

```
GENERAL INFORMATION SECTION
-------------------------------------------------------------------------------
Tuning Task Name   : staName14054
Tuning Task Owner  : HRDEMO
Tuning Task ID     : 9295
Workload Type      : Single SQL Statement
Execution Count    : 1
Current Execution  : EXEC_9255
Execution Type     : TUNE SQL
Scope              : COMPREHENSIVE
Time Limit(seconds): 1800
Completion Status  : COMPLETED
Started at         : 04/19/2012 07:33:50
Completed at       : 04/19/2012 07:33:50

-------------------------------------------------------------------------------
Schema Name: HRDEMO
SQL ID     : 028hrurkuc6ah
SQL Text   : SELECT SUM(E.Salary),
               AVG(E.Salary),
               COUNT(1),
               E.Department_Id
             FROM Departments D,
               Employees E
             GROUP BY E.Department_Id
             ORDER BY E.Department_Id

-------------------------------------------------------------------------------
FINDINGS SECTION (1 finding)
-------------------------------------------------------------------------------

1- Restructure SQL finding (see plan 1 in explain plans section)
----------------------------------------------------------------
  An expensive cartesian product operation was found at line ID 2 of the
  execution plan.

  Recommendation
  --------------
  - Consider removing the disconnected table or view from this statement or
    add a join condition which refers to it.

-------------------------------------------------------------------------------
EXPLAIN PLANS SECTION
-------------------------------------------------------------------------------

1- Original
-----------
Plan hash value: 2187233893

 
---------------------------------------------------------------------------------------
| Id  | Operation               | Name        | Rows  | Bytes | Cost (%CPU)| Time     |
---------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT        |             |    11 |    77 |    35   (3)| 00:00:01 |
|   1 |  SORT GROUP BY          |             |    11 |    77 |    35   (3)| 00:00:01 |
|   2 |   MERGE JOIN CARTESIAN  |             |  2889 | 20223 |    34   (0)| 00:00:01 |
|   3 |    TABLE ACCESS FULL    | EMPLOYEES   |   107 |   749 |     3   (0)| 00:00:01 |
|   4 |    BUFFER SORT          |             |    27 |       |    32   (4)| 00:00:01 |
|   5 |     INDEX FAST FULL SCAN| DEPT_ID_PKX |    27 |       |     0   (0)| 00:00:01 |
---------------------------------------------------------------------------------------
 
Query Block Name / Object Alias (identified by operation id):
-------------------------------------------------------------
 
   1 - SEL$1
   3 - SEL$1 / E@SEL$1
   5 - SEL$1 / D@SEL$1
 
Column Projection Information (identified by operation id):
-----------------------------------------------------------
 
   1 - (#keys=1) "E"."DEPARTMENT_ID"[NUMBER,22], COUNT(*)[22], 
       COUNT("E"."SALARY")[22], SUM("E"."SALARY")[22]
   2 - (#keys=0) "E"."SALARY"[NUMBER,22], "E"."DEPARTMENT_ID"[NUMBER,22]
   3 - "E"."SALARY"[NUMBER,22], "E"."DEPARTMENT_ID"[NUMBER,22]
   4 - (#keys=0) 

-------------------------------------------------------------------------------
```

  
For doing this without SQL Developer, there are several things which you need to do. I have a little graphic which looks at each of the steps which need to be taken to create a tuning job in the normal SQL\*Plus interface.  The main steps are creating task tuning tasks, and then interpreting the output.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqVOXWIsMoD9L2qNR5fwyqgAq5VdfBISANePPgYVq_AYksf-cTSBZF9g96K7aHN0nM1zdLLFZf2viQpRPsl7QfiN9DqTs3-adhZitVRMadzDCdOqCkJ5DctN4TksJs6qGFOZTR3lQAWJc/s320/Screen+Shot+2012-04-19+at+11.10.21.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqVOXWIsMoD9L2qNR5fwyqgAq5VdfBISANePPgYVq_AYksf-cTSBZF9g96K7aHN0nM1zdLLFZf2viQpRPsl7QfiN9DqTs3-adhZitVRMadzDCdOqCkJ5DctN4TksJs6qGFOZTR3lQAWJc/s1600/Screen+Shot+2012-04-19+at+11.10.21.png)

Finally, this functionality is part of the SQL Worksheet in SQLDeveloper, which together with trace file editing, explain plan and autotrace, hierarchical profiler and monitoring sessions adds more tools to the toolbox for trying to find issues with you code.
