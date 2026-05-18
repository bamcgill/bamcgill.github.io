---
title: "Application Migration - Part 2"
date: 2012-03-22 18:21:00 +0000
last_modified_at: 2012-03-22 18:21:01 +0000
---

In our previous post, [Application Migration -Part 1](http://barrymcgillin.blogspot.com/2012/03/application-migration-part-1.html), we introduced application migration for change of database.  In the examples, we cited Sybase to Oracle.  In this post, we will introduce the way we can scan the application for items of interest and report on those with [Oracle SQLDeveloper](http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html).  In our third post, we will replace and translate the items found so we can run the application in Oracle.  
  
Since  SQL Developer 3.1 we have had the ability to scan source files and replace the items we find with appropriate changes.   
  
The application migration functionality uses XML rules to define the type of files to be scanned and the type of changes which should be made.  The tool uses regular expressions defined in XML to scan the application.  Lets look at these in stages.  There are a few parts of the tool which needs to be defined.  
  

1. Recognizer - A recognizer is used to identify the types of files which are supported.
2. Rules - Rules are ways to define regular expressions which can identify your statements or clauses that you want to identify
3. Replacements - what types of replacements you want to do. We can do the following

1. Text replacement: Replace the item found by the with another string
2. Translator: Use a built in translator from SQL Developer to translate the string identified
3. Script replacement: Use Javascript, or others like ruby or groovy
4. Class Replacement: Use a custom class to translate the string found.

Without a recognizer, scanning a directory will give us this.

```
migration.sh -actions=scan -dir=/blog/src/
```

```
------------------------    Summary   -----------------------
High Level Overview
-------------------
        0 total calls found
        0 distinct calls found
        0 files scanned
        0 language types
        1 total files in source
        0 lines of code in scanned application
-------------------------------------------------------------
```

Here, the scanner is telling us, it found our test file, but doesn't know what to do with it. So, we can start with defining a recognizer to do that.

  

```
<rulesfile version="1.0" name="Shell file recognizer"
    description="Recognize .sh files">
    <!-- This recognizer will identify a shell script file. This will be used 
        by the scanner to identify a shell script. Using this recognition, any registered 
        rules will be used on this a shell script to do translation. -->
    <recognizer name="sh" description="sh recognizer" enable="true">
        <fileExtension extension="sh" />
        <expression><![CDATA[\#\!\/bin\/sh]]></expression>
    </recognizer>
</rulesfile>
```

  
So, now we can use the recognizer to identify the type of file.  

```
Migration.sh -actions=scan -dir=/blog/src -rulesdir=/blog/rules -type=sybase
```

```
File Type Summary
----------------------
         sh      1 file

-------------------------------------------------------------
------------------------    Summary   -----------------------
High Level Overview
-------------------
        0 total calls found
        0 distinct calls found
        0 files scanned
        1 language types
        1 total files in source
        0 lines of code in scanned application
-------------------------------------------------------------
```

Now, we can see the scanner knows what type of file it has.  It can now use that type to identify rules which we will specify to identify the items in the file.   

```
    <ruleset name="sample rules" enable="true" type="SYBASE"
        description="" source="sh" codetype="sql">
        <required>
            <regex>
                <expression><![CDATA[select]]></expression>
            </regex>
        </required>
        <rules>
            <regex>
                <expression><![CDATA[select.*\n]]></expression>
            </regex>
        </rules>
    </ruleset>
```

For a rules file, we need to define a ruleset which contains the rules.  There are two parts to it, a required section and a rules section.  The required section defines an expression which will be used to test the file to see if we should use the rules that are defined.  In this case, we have just defined a keyword to identify before we look at anything.  The rules section then defines some expressions which are used to identify some statements.  In this example, we have a select statement expressions which is really simple to illustrate the point.  
The other interesting points here are the 'source'  attribute on the ruleset which defines the type of source files these rules should be used against. The second one is the 'type' attribute which defines the database type for the application.  
We can either have two files with a recognizer in one and rules in another.  Or, you can merge the rules and the recognizer in one <rulesfile>  
  
We can use the same command as earlier to scan with these rules now to see if we find something in the file. Now,  I have added other rules which search for each artifact to be changed, but the process is the same.  

```
Migration.sh -actions=scan -dir=/blog/src -rulesdir=/blog/rules -type=sybase
```

 and now we get these results.  

```
-------------------------------------------------------------
Call Breakdown Summary
----------------------
        3:      go
        1:      select count(*) from authors
        1:      select top 5 au_lname,au_fname,postalcode from authors
        1:      use pubs2
        1:      isql -Usa -P -SSLC01PAP <<EOF

File Type Summary
----------------------
         sh      1 file

------------------------    Summary   -----------------------
High Level Overview
-------------------
        7 total calls found
        5 distinct calls found
        1 files scanned
        1 language types
        1 total files in source
        12 lines of code in scanned application
-------------------------------------------------------------
```

  
So, we now have found all the statements identified that we want to translate or change for the translation.  
  
In Summary, we have defined a recognizor to identify the file types we want to look at, we've defined some rules to identify the things we want to change.  
  
Running the scanner with these rules against our source file, we showed in [Application Migration -Part 1](http://barrymcgillin.blogspot.com/2012/03/application-migration-part-1.html), we have found several things to change.  In the next instalment, we'll show you how to change the things you found to run against our oracle database.
