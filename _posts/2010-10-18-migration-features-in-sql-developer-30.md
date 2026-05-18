---
title: "Migration Features in SQL Developer 3.0"
date: 2010-10-18 19:34:00 +0000
last_modified_at: 2010-10-18 21:14:22 +0000
tags:
  - 3.0
  - Migration
  - SQL Developer
---

Since we released 2.1, we've worked with several customers and have added several great new features which have helped these customers increase the automation within their migration and the information they receive about it.

Here's a quick breakdown and we'll delve into these in later posts.

[**Command line interface**](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHw-FFsvQE8UP778VR_H3gEDeeEThOyRj8wuMSeN4GU1SYLgOXb3xE06fUdehP7HYIv2XCCWKYUTnLbEk0BKCtsNXZgOEBQeYx5ASd2_aetjv6ZmlzopPrdIL0erRfRpWGD4tX0eWM6C0/s1600/cndline-ovrview.PNG)

Most customers are looking to use a command line interface to do at least some of the migration for them, These can include all the steps that SQL Developer supports:

- Capture - Connect to a source database, scan the data dictionary and create an independent model of the source.
- Analyze - Analyze the model and report on what the source database contains and what issues there might be in it which need manual intervention
- Convert to Oracle. - Convert the source model into its Oracle equivilent.
- Generate Oracle Model - From the converted model, the user can generate the DDL for all the new schema in his database including all PLSQL
- Build new database - The tool can run the sql produced and report on the errors which were found, even correlating between objects in the source and objects in the target
- Move data - You can move data in two ways, either connected to the target database or you can generate unload files for the source database and SQL\*Loader scripts to load this into Oracle

**Enterprise Capture**

This new feature allows the user to point at a server and capture all the databases in that server. This has been tested on Servers with up on 100 databases, captured and processed in minutes. Its one of the biggest requests we have had over the last few releases and this makes multi schema migration a breeze.

**Application Scanning**

In 3.0 we have introduced the concept of applications tied to databases. For this release we have focused on ctlib and dblib programs. Today, we can find all sybase calls in any program. We generate details reports on the contents of your application which provide information on size and complexity of the migration problem.

**Estimation Reports**

3.0 has introduced extensive database reports on the migration. Specifically, the reports include

- High level object summary
- High level error summary
- Detailed error summary
- Detailed object size summary
- Detailed comparison between source objects, capture and converted objects and the new Oracle object
- Temporary table usage

**Migration Project Navigator**

3.0 has also introduced a brand new project concept for Migration Projects. This is a new navigator which holds all the servers in a project all together. This has the benefit of being able to run several projects together, but report centrally on any one of them at any time with detailed information.

**Migration Wizard**

In 3.0, we have changed the quick migrate wizard to be a generic multi entry, single source of true path through a migration. This replaces the whole Quick Migrate concept and is now the only way to do a migration with the tool.

****Parser and Translation enhancements**

A lot of work has gone into fixing issues within the translators so they can perform in a better way and produce more consistent output. We are continuing to improve this with each release.**

**Copy to Oracle**

Lastly, we have a new concept on all the third party navigators which is called "Copy to Oracle". This allows the user to copy tables and procedures from third parties into an oracle schema, without a migration repository.
