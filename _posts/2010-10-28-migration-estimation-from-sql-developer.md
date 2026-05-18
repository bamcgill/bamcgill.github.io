---
title: "Migration Estimation from SQL Developer"
date: 2010-10-28 10:15:00 +0000
last_modified_at: 2010-10-28 11:13:05 +0000
tags:
  - Migration Workbench SQL Developer
  - database migration
---

Last post we mentioned all the features of 3.0 for migration. This one, we're taking it a bit further and looking at the overview of the migration project itself.

For most users, the main thing they want to know is how much of the migration will be completed automatically. We've introduced a new spreadsheet which gets generated from the repository and gives a birds eye view of your database servers and your applications which are being migrated.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEipN8ZXGnSfYGMjJ2SoqYaJJ8DtCmRYh6O3OWF3iTAEJtvF9hsKN9K00b7F8Qzif8MuzjTWoXdxdApVLJra3OexVhVGTUnFv8DZqArDIGnW9eZvC_VChVv8ct6TRyzGF1uIjGfGkTZIgq0/s200/migration_projects.PNG)

Here we have a number of migration projects in the migration navigator which are Sybase, SQL Server and DB2. We have converted all three and need to know how much of the migration the tools can do.

Very simply, we can right click on the top projects node, or any individual project node and choose to "create an estimation plan". This will generate a spreadsheet with the detail of the project with a high level summary of the state of the project.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhrYp-TGlhuuzafBP2nFA74k4PdE1NNI0j_zGHzPrZ-WIQHGZ2-IBnkQ7QmN_-QTxEIGG5V56x288PadUr2NT0OvULBwYK3qdhak9GjmGk3PShMnUtfJ4ykW8WJOSLZr_7RtoHc-PCwX8c/s200/estimationPlan.png)

On the summary page, there are 4 different graphs. The top two deal with the databases being migrated and how much automation the tool can provide. Specifically, they show how many objects failed as part of the migration and which area the failures occured in. The bottom two show the applications which have been scanned and show what percentage of the files which make up the application have database calls which need to be changed. This example shows the Sybase ctlib sample applications, the most of which have things to change.

This represents the first page of the migration plan. Each of the other pages in the plan break down the database migration into tables, stored procedures, triggers and view detail. The user is allowed to add specifics for their organisation which will help put together a project estimate of how long it will take and how much resource it will take to bring the database migration project to a production state.
