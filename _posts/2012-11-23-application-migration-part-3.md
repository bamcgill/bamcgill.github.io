---
title: "Application Migration - Part 3"
date: 2012-11-23 18:09:00 +0000
last_modified_at: 2012-11-23 18:11:56 +0000
tags:
  - SQL*Plus
  - application Migration
  - SQL Developer
  - command line
---

Ok, Finally, we have got to part 3 of Application Migration.  In [Part 1](http://barrymcgillin.blogspot.co.uk/2012/03/application-migration-part-1.html), we outlined a program which runs in Sybase through iSQL.  We then followed this, in [part 2](http://barrymcgillin.blogspot.com/2012/03/application-migration-part-1.html) with 2 important pieces.  

1. Recognizers to identify the file types of the source we post
2. Rules to identify items within the files and report on the them

In this part, We will take the rules we used for the previous part, and add some replacement rules.  So, lets recap.  Our recogniser is set for shell files as below.

```
<?xml version="1.0" encoding="UTF-8"?>
<rulesfile version="1.0" name="Shell file recognizer" description="Recognize .sh files">
  <recognizer name="sh" description="sh recognizer" enabled="true">
    <fileExtension extension="sh" />
    <expression><![CDATA[#!/bin/sh]]></expression>
  </recognizer>
</rulesfile>
```

Our rules file is now extended to include replacement rules.  Looking at the rules file below, we have the two main sections  

1. The required section, which defines the expressions which are used to see if we should scan a file
2. Rules section which can have 3 sections

1. Example clause which contains the expression which shows what should be found by the rule.
2. Expression clause which defines a regular expression which is used to identify the items to be change
3. Replacement clause which can be configured in 3 different stances to cope with different replacements.

Review the file below:

  

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="../schema/scanner.xsd"?>
<rulesfile version="1.0" name="Sample sh scanner rules"
    description="Sample rules to show whats possible" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="../../schema/scanner.xsd">
    <ruleset name="isql sample rules" enable="true" type="SYBASE"
        description="" source="sh" codetype="isql">
        <required>
            <regex>
                <expression><![CDATA[go|isql]]></expression>
            </regex>
        </required>
        <rules>
            <regex>
                <expression><![CDATA[go *\n]]></expression>
                <replacement type="text"><![CDATA[]]>
                </replacement>
            </regex>
            <regex>
                <expression><![CDATA[use.*\n]]></expression>
                <replacement type="regex"><![CDATA[]]>
                </replacement>
            </regex>
            <regex>
                <expression><![CDATA[isql.*EOF]]></expression>
                <replacement type="regex"><![CDATA[sqlplus barry/barry <<EOF]]></replacement>
            </regex>
        </rules>
    </ruleset>
    <ruleset name="sql sample rules" enable="true" type="SYBASE"
        description="" source="sh" codetype="sql">
        <required>
            <regex>
                <expression><![CDATA[select]]></expression>
            </regex>
        </required>
        <rules>
            <regex>
                <expression><![CDATA[select.*\n]]></expression>
                <replacement type="translator"/>
            </regex>
        </rules>
    </ruleset>
</rulesfile>
```

  
The replacement tags are  

1. Text

- This is the simplest type of replacement, taking the source strings found and replacing them with the string in the replacement tag.

2. regex

- The regular expression replacement can either simply replace text, or it can also use regular expressions to rearrange the string that was found.  For example,  function(a,b,c) can be switched to myfunction(c,a,b)

3. Translator

- The translator type allows the user to take the string found and pass it to a language translator denoted by the type.  In our example, the type is SYBASE, which will call our sybase translator and translate the source string.

In the rules file above, we have 2 rulesets defined, the first doing text and regex replacements, and the second doing translator replacements.  All these can be mixed together, though.  If you have a lot of rules, it makes sense to delineate them in rulesets so the tool can filter out what is not required.  
Now, taking a look at the source we had in Part 1  
  

```
bamcgill-macbook-pro:src bamcgill$ cat test.sh
#!/bin/sh
isql -UMYUSER -PMYPASS -SMYSERVER <<EOF
use pubs2
go
select count(*) from authors
go
select top 5 au_lname,au_fname,postalcode from authors
go
EOF
bamcgill-macbook-pro:src bamcgill$
```

  
we can now run the scanner and make the replacements.  Using a similar command to the that used in part 1, We can replace code in this script.  
  

```
bamcgill-macbook-pro:demo bamcgill$ migration -actions=scan -dir=/Users/bamcgill/code/demo/src -rulesdir=/Users/bamcgill/code/demo/rules -inplace=true
```

  
Now, we when we look at the file, test.sh again, we have  
  

```
#!/bin/sh
sqlplus barry/barry <<EOF
SELECT COUNT(*) 
  FROM authors ;

SELECT au_lname ,
       au_fname ,
       postalcode 
  FROM authors  WHERE ROWNUM <= 5;

EOF
```

  
So, there we a translated file which was running iSQL on Sybase, but is now running SQL\*Plus and Oracle specific SQL.  
  
Now, if you are interested, heres what the scanner said as it was running.  It prints out individual statements as they are found and where in the source they were found. At the end, the tool summarises what was found and where.  

```
bamcgill-macbook-pro:demo bamcgill$ migration -actions=scan -dir=/Users/bamcgill/code/demo/src -rulesdir=/Users/bamcgill/code/demo/rules -inplace=true

Oracle SQL Developer
 Copyright (c) 1997, 2011, Oracle and/or its affiliates. All rights reserved. 

Finding files....
Default Application Name

                test.sh
                        3:go

                        5:go

                        7:go

                        2:use pubs2

                        1:isql -UMYUSER -PMYPASS -SMYSERVER <<EOF
                        2:select count(*) from authors

                        3:select top 5 au_lname,au_fname,postalcode from authors

------------------------ Application Results -----------------

Call Breakdown Summary by File
------------------------------
/Users/bamcgill/code/demo/src/test.sh
        3:      go

        1:      use pubs2

        1:      isql -UMYUSER -PMYPASS -SMYSERVER <<EOF
        1:      select count(*) from authors

        1:      select top 5 au_lname,au_fname,postalcode from authors

-------------------------------------------------------------

Call Breakdown Summary
----------------------
        3:      go

        1:      use pubs2

        1:      isql -UMYUSER -PMYPASS -SMYSERVER <<EOF
        1:      select count(*) from authors

        1:      select top 5 au_lname,au_fname,postalcode from authors

-------------------------------------------------------------

File Type Summary
----------------------
         sh      1 file

-------------------------------------------------------------
------------------------    Summary   -----------------------
High Level Overview
-------------------
        7 total calls found
        5 distinct calls found
        1 files scanned
        1 language types
        2 total files in source
        9 lines of code in scanned application
-------------------------------------------------------------
-------------------------------------------------------------
scan completed successfully
```

If you want to know more about this, drop me line on twitter [@bamcgill](https://twitter.com/bamcgill), or by email on barry.mcgillin@oracle.com  
  
You can download [SQL Developer](http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html) from [OTN](http://www.oracle.com/technetwork/index.html).
