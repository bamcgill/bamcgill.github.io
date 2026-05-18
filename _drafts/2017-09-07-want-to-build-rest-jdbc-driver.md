---
title: "Want to build a REST JDBC Driver"
date: 2017-09-07
---

We have been working hard to produce our first cut of the [REST JDBC Driver](http://www.oracle.com/technetwork/developer-tools/rest-data-services/downloads/index.html) for use with [Oracle REST Data Services 17.3.0](http://www.oracle.com/technetwork/developer-tools/rest-data-services/downloads/index.html).  We are publishing the driver as Opensource and will have a repository on Github later which will have the code for several libraries you can use.  In the meantime, before I publish this there, We have two zips of source code you can play with and buid. Both are really easy to setup.  
  
Go to our [DBTools Github page on OTN](http://www.oracle.com/technetwork/developer-tools/sql-developer/learnmore/github-projects-3875948.html). In there you'll find two zip files of source under the heading of **DBTools Common Project**.  
  

- [REST\_JDBC\_SOURCE.zip](http://download.oracle.com/otn/java/ords/REST_JDBC_SOURCE.zip)
- [REST\_JDBC\_EXAMPLES.zip](http://download.oracle.com/otn/java/ords/REST_JDBC_EXAMPLES.zip)

The REST\_JDBC\_SOURCE.zip contains the source of the driver and the REST\_JDBC\_EXAMPLES.zip contains individual examples of using JDBC Driver API, from Connections to ResultSets.

You will need to download [SQLcl from OTN](http://www.oracle.com/technetwork/developer-tools/sqlcl/downloads/index.html) and copy the zip file into the source directory in order to build, then just run ant and it will build the REST JDBC jar file for you.

```
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~) $unzip -qq REST_JDBC_SOURCE.zip 
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~) $cp sqlcl-17.2.0.184.1230-no-jre.zip source
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~) $cd source
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~/source) $ant
Buildfile: /Users/bamcgill/source/build.xml

clean:

unzip_sqlcl:
     [echo] Download SQLcl Beta [sqlcl-17.2.0.184.1230-no-jre.zip] from OTN to this directory
    [unzip] Expanding: /Users/bamcgill/source/sqlcl-17.2.0.184.1230-no-jre.zip into /Users/bamcgill/source

compile:
    [mkdir] Created dir: /Users/bamcgill/source/built/classes
    [javac] Compiling 41 source files to /Users/bamcgill/source/built/classes
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/BLOB.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/CLOB.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/CallableStatement.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/Connection.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/DatabaseMetaData.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/Driver.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/ParameterMetaData.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/PreparedStatement.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/ResultSet.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/ResultSetMetadata.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/RowId.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/Statement.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/Driver.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/NotImplementedException.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestCallableStatement.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestCallableStatementImpl.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestConnection.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestPreparedStatement.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestPreparedStatementImpl.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestResultSet.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestStatement.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestStatementImpl.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/orest/ORestjdbcResources.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/package-info.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/Accessor.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/DateTimestampsUtil.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/Defaults.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/ExceptionUtil.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/JDBCClient.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/JDBCSessionType.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/LogUtil.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/OracleTypes.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/OracleTypesSize.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/RestJdbcNotImplementedException.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/RestJdbcOutputStream.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/RestJdbcUnsupportedOperationException.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/RestJdbcWriter.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/RestjdbcResources.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/RestjdbcSqlWarnings.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/SQLStateMapping.java
    [javac] /Users/bamcgill/source/src/oracle/dbtools/jdbc/util/package-info.java
    [javac] Note: Some input files use or override a deprecated API.
    [javac] Note: Recompile with -Xlint:deprecation for details.
    [javac] Creating empty /Users/bamcgill/source/built/classes/oracle/dbtools/jdbc/package-info.class
    [javac] Creating empty /Users/bamcgill/source/built/classes/oracle/dbtools/jdbc/util/package-info.class

jar:
     [copy] Copying 1 file to /Users/bamcgill/source/built/classes
      [jar] Building jar: /Users/bamcgill/source/built/oracle.dbtools.jdbcrest.jar

BUILD SUCCESSFUL
Total time: 2 seconds
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~/source) $
```

Similarly with the examples, unzip the zip file and copy the sqlcl-17.2.0.184.1230-no-jre.zip into the examples directory and run ant in there as shown below.

```
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~) $unzip -qq REST_JDBC_EXAMPLES.zip 
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~) $cp sqlcl-17.2.0.184.1230-no-jre.zip ./examples/
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~) $cd examples
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~/examples) $ant
Buildfile: /Users/bamcgill/examples/build.xml

clean:

unzip_sqlcl:
     [echo] Download SQLcl [sqlcl-17.2.0.184.1230-no-jre.zip] from OTN to this directory
    [unzip] Expanding: /Users/bamcgill/examples/sqlcl-17.2.0.184.1230-no-jre.zip into /Users/bamcgill/examples

compile:
    [mkdir] Created dir: /Users/bamcgill/examples/built/classes
    [javac] Compiling 11 source files to /Users/bamcgill/examples/built/classes
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/examples/BasicExample.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/examples/CreateDropTable.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/examples/DateTimeExample.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/examples/GetURL.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/examples/PreparedStatementBatchExample.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/examples/PreparedStatementExample.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/examples/StatementPaginationExample.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/orest/examples/CreateStatementExample.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/orest/examples/PreparedStatementExample.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/orest/examples/PreparedStatementExample2.java
    [javac] /Users/bamcgill/examples/src/oracle/dbtools/jdbc/orest/examples/ResultSetExample.java

BUILD SUCCESSFUL
Total time: 1 second
(bamcgill@daedalus.home)–(0|ttys000|-bash)
(~/examples) $
```
