---
title: "Tracing your SQL Session with SQL Developer"
date: 2012-04-19
---

Getting information about what is happening with your query or queries are getting easier these days.  Today,   I am going to show you how to generate a trace file in Oracle and how to open it up and view it. There are other tools around which can do this too, but its one of those features which Kris added yonks ago and I ended up demoing it yesterday, so here we go.  
  
If you have a sqlplus sesstion, or even a sqlworksheet running in SQLDeveloper,   you can switch on tracing with the following command  
  

```
alter session set sql_trace = true;
```

  
When we have done this we can run some sql.  I've tried to make it  a little bit more fun by doing it for sys and querying the hr schema.  I've spent a little bit of time setting up my test query, going from the simple to the little more advanced.  

```
SELECT SUM(E.Salary),
  Avg(E.Salary),
  Count(1),
  E.Department_Id
FROM 
  Employees E
Group By E.Department_Id;
```

We can get our results and work through them as normal, then we can switch tracing off again
