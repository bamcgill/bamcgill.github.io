---
title: "Run your SQL script from java NOW"
date: 2018-04-13 21:18:00 +0000
last_modified_at: 2018-04-13 21:18:44 +0000
tags:
  - Java
  - dbtools-common
  - open source
  - oracle
  - maven
  - Database Tools
---

Run them with the code we use for Oracle SQL Developer, SQLcl and REST Data Services.  
We've just released some of the code that underpins these tools in an attempt to help  others run SQL, PLSQL and SQL\*Plus scripts confidently and repeatably from java.  
  
From Github, look for the repository [dbtools-commons](https://github.com/oracle/dbtools-commons). Look at my [previous post](http://barrymcgillin.blogspot.co.uk/2018/04/sqlcl-code-aka-dbtools-common-is-now.html) to build it.  
  
The code below is one simple example to run sql code with the common jars we ship with sqlcl and sqldeveloper.  
  
Further down, I stuck in a pom file you can use to build with maven.  
  

## Demo using Script executor to run SQL

  

```
1:  import java.io.BufferedOutputStream;  
2:  import java.io.ByteArrayOutputStream;  
3:  import java.io.UnsupportedEncodingException;  
4:  import java.sql.Connection;  
5:  import java.sql.DriverManager;  
6:  import java.sql.SQLException;  
7:  import oracle.dbtools.db.ResultSetFormatter;  
8:  import oracle.dbtools.raptor.newscriptrunner.ScriptExecutor;  
9:  import oracle.dbtools.raptor.newscriptrunner.ScriptRunnerContext;  
10:  /**  
11:   * @author bamcgill  
12:   */  
13:  public class DemoScriptRunner {  
14:    /**  
15:     * @param args  
16:     * @throws ClassNotFoundException  
17:     * @throws SQLException  
18:     * @throws UnsupportedEncodingException  
19:     */  
20:    public static void main(String[] args) throws ClassNotFoundException, SQLException, UnsupportedEncodingException {  
21:      Class.forName("oracle.jdbc.driver.OracleDriver");  
22:      Connection conn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521/ORCL", "barry", "oracle");  
23:      ScriptRunnerContext ctx = new ScriptRunnerContext();  
24:      ctx.setBaseConnection(conn);  
25:      ScriptExecutor executor = new ScriptExecutor(conn);  
26:      ByteArrayOutputStream bout = new ByteArrayOutputStream();  
27:      BufferedOutputStream bs = new BufferedOutputStream(bout);  
28:      executor.setOut(bs);  
29:      executor.setScriptRunnerContext(ctx);  
30:      executor.setStmt("select * from all_objects where rownum < 10 ");  
31:      ResultSetFormatter.setMaxRows(Integer.MAX_VALUE);  
32:      executor.run();  
33:      String results = bout.toString("UTF8");  
34:      System.out.println(results);  
35:    }
```

  

## Pom File to build Code

```
1:  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
2:      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
3:      <modelVersion>4.0.0</modelVersion>  
4:      <groupId>oracle.dbtools</groupId>  
5:      <artifactId>demo-common</artifactId>  
6:      <version>0.0.1-SNAPSHOT</version>  
7:      <packaging>jar</packaging>  
8:      <name>demo-common</name>  
9:      <url>http://maven.apache.org</url>  
10:      <properties>  
11:          <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  
12:      </properties>  
13:      <dependencies>  
14:          <dependency>  
15:              <groupId>junit</groupId>  
16:              <artifactId>junit</artifactId>  
17:              <version>3.8.1</version>  
18:              <scope>test</scope>  
19:          </dependency>  
20:          <dependency>  
21:              <groupId>oracle.dbtools</groupId>  
22:              <artifactId>dbtools-common</artifactId>  
23:              <version>LATEST</version>  
24:          </dependency>  
25:          <dependency>  
26:              <groupId>com.oracle.jdbc</groupId>  
27:              <artifactId>orai18n</artifactId>  
28:              <version>12.2.0.1</version>  
29:          </dependency>  
30:          <dependency>  
31:              <groupId>com.oracle.jdbc</groupId>  
32:              <artifactId>orai18n-mapping</artifactId>  
33:              <version>12.2.0.1</version>  
34:          </dependency>  
35:      </dependencies>  
36:  </project>
```
