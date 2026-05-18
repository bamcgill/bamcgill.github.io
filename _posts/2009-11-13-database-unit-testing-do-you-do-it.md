---
title: "Database Unit Testing:- Do you do it?"
date: 2009-11-13 17:13:00 +0000
last_modified_at: 2009-11-14 14:33:50 +0000
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQUt-m2qc5HD2Ryf5Qj5dplyXhyphenhyphenXdx_0yzLR68OYanIaht0tFiviQMOEtQfhpdDj5c0k2JhGBc2yPHxw27n_BToXWEvOOuQiRkdL1ze0QPuEdI12sNWAJZXHoGBByg6eyhbmojxtPOHiA/s200/UTNAV.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQUt-m2qc5HD2Ryf5Qj5dplyXhyphenhyphenXdx_0yzLR68OYanIaht0tFiviQMOEtQfhpdDj5c0k2JhGBc2yPHxw27n_BToXWEvOOuQiRkdL1ze0QPuEdI12sNWAJZXHoGBByg6eyhbmojxtPOHiA/s1600-h/UTNAV.JPG)  
Testing. When you're writing code, how often do you test it? Ok, you test it, but how often do you spend the time to put a set of discrete tests together to make sure that your code is doing what you thought it would do and moreover, it doesnt do what its not supposed to.  
  
As part of SQL Developer 2.1, Unit Testing is one of the main features we have added. This is very different to anything you've seen in this area before. There are 5 different things on the new navigator we have added.  
  

1. Tests: These are individual or discreate tests against a piece of code like a stored procedure or a function or package. Each test can have several implementations of the test. I.e., if it is a stored procedure, you can have an implementation with n implementation depending on the permutations of the paramters that you want to support.
2. Suites: This is a regular concept, like JUnit, which you can use to group your tests and run them together, in sequence. In fact, with 2.1, you can run unit tests from the command line which means you can hook them up with your build machine and run these in as part of a standard build and publish results with your builds
3. reports: We have canned several reports so you can see how your suite of tests ran, what the coverage numbers are and allow you to drill through each implementation that was run.
4. Lookups: Lookups are setup to allow you to predefine static parameter values that can be group by functional need and used in test implementations.
5. Libraries: Like the word says, these are libraries of startups, teardowns, validations, and defined dynamic values that we want to use regularly in tests.

  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgr2ibf4O7AQo01Kq4kxjMnDinQEySd6QN4FwT-S9OV0WCW8bF3_JqLruJ_o2cO2OYR54ut9xsVt10qo15Z4aNqsWMWLbsROiWPUaHU9UeJn3oc8Gaw4qZBTWooWgLkMoWgsGyysXYO9gI/s200/UTIMP.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgr2ibf4O7AQo01Kq4kxjMnDinQEySd6QN4FwT-S9OV0WCW8bF3_JqLruJ_o2cO2OYR54ut9xsVt10qo15Z4aNqsWMWLbsROiWPUaHU9UeJn3oc8Gaw4qZBTWooWgLkMoWgsGyysXYO9gI/s1600-h/UTIMP.JPG)The test here shows each implementation of the test. The implementation is a set of parameters which will give you a specific result, based on processing the parameters as part of the stored procedure.  
  
This is our first release of Unit Testing and we will add more features in the next few releases. This release allows you to set up suites of tests with parameters covered by all the scalar datatypes. We will cover more abstract types in future releases.  
  
This is available as part of SQL Developer 2.1, which at time of writing this is available as an EA from http://otn.oracle.com/sqldeveloper. Download it and play with it. If there are things you like, let us know and if there are things you would like added, then you can let us know on the feature request page as usual which is http://sqldeveloper.oracle.com  
  
![](file:///C:/DOCUME%7E1/bamcgill/LOCALS%7E1/Temp/moz-screenshot-4.jpg)
