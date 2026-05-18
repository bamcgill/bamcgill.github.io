---
title: "SQLcl code aka DBTools Common is now open source "
date: 2018-04-13
tags:
  - Java
  - open source
  - oracle
  - common
  - GitHub
  - Database Tools
  - dbtools
  - sqlcl
---

So Gerald has just flipped the switch and we have officially open sourced the code behind Oracle SQLDeveloper and SQLcl  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjELBA6geyW5JwxCpg27amjSldjAmcj-M86bFFLKOdtetxoNGYLUwxrmXSzrJp8_0SsVc1Cz6cdKyYynhiJuV1_yIH20_HWhIDul5_k8K0G-78Yvq8dW9qaTZKma4U-luaEvbuMlNuvzRY/s400/Screen+Shot+2018-04-13+at+19.13.22.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjELBA6geyW5JwxCpg27amjSldjAmcj-M86bFFLKOdtetxoNGYLUwxrmXSzrJp8_0SsVc1Cz6cdKyYynhiJuV1_yIH20_HWhIDul5_k8K0G-78Yvq8dW9qaTZKma4U-luaEvbuMlNuvzRY/s1600/Screen+Shot+2018-04-13+at+19.13.22.png)

  
As he says on twitter, this is on Github and the repository is called dbtools-commons.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjntODrC4ijCJ_az_XcbYg4S6OjHu1dQRS2uArvJY4wuRpqtDewmXX1opCUKjlO98ZuDb-MJWSIr_IP2u-7X7vNnPXcKjFxUNchhFDKJ-jxVH3MtVtPQfzrVKCsqLOzNOfQYiAPIcgjw6w/s400/Screen+Shot+2018-04-13+at+19.12.40.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjntODrC4ijCJ_az_XcbYg4S6OjHu1dQRS2uArvJY4wuRpqtDewmXX1opCUKjlO98ZuDb-MJWSIr_IP2u-7X7vNnPXcKjFxUNchhFDKJ-jxVH3MtVtPQfzrVKCsqLOzNOfQYiAPIcgjw6w/s1600/Screen+Shot+2018-04-13+at+19.12.40.png)

As I mentioned in the last post, you can [download 18.1.1 of SQLcl](http://www.oracle.com/technetwork/developer-tools/sqlcl/downloads/index.html) and install the jars as dependencies to build this project.  
  
To get started with this code base, here is a quick script to build it for you. This will unpack the 18.1.1 zip, run the install, then clone the dbtools-commons repository, and build it.  
  
  

|  |  |
| --- | --- |
| ```  1  2  3  4  5  6  7  8  9 10 11 12 ``` | ``` (    rm -rf sqlcl && rm -rf /tmp/m2 &&    unzip dbtools-sqlcl-18.1.1-sqlcl.zip &&    cd sqlcl/lib &&    mvn -Dmaven.repo.local=/tmp/m2 validate &&    cd - &&    rm -rf dbtools-commons/ &&    git clone git@github.com:oracle/dbtools-commons.git &&    cd dbtools-commons &&    mvn -Dmaven.repo.local=/tmp/m2 install &&    cd -  ) > build.log 2>&1 ``` |

  
Now, if you have never run maven before, this will take a while, as maven needs to download all the plugins to do the build and the dependencies required to complete the build.  
  
With a bit of luck (especially today on Friday 13th, it should start like this:  
  

|  |  |
| --- | --- |
| ``` 1 2 3 4 5 6 7 ``` | ``` Archive:  dbtools-sqlcl-18.1.1-sqlcl.zip    creating: sqlcl/   inflating: sqlcl/lib/orai18n.jar      inflating: sqlcl/lib/commons-logging.jar     inflating: sqlcl/lib/orai18n-mapping.jar     inflating: sqlcl/lib/dbtools-sqlcl.jar     inflating: sqlcl/bin/sql.exe ``` |

  
and should end like this:  
  
  

|  |  |
| --- | --- |
| ```  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 ``` | ``` [INFO] --- maven-install-plugin:2.3.1:install (default-install) @ hudsonplugin --- [INFO] Installing /Users/bamcgill/work/sandbox/dbtools-commons/hudsonplugin/target/hudsonplugin.hpi to /tmp/m2/oracle/dbtools/hudsonplugin/1.0-SNAPSHOT/hudsonplugin-1.0-SNAPSHOT.hpi [INFO] Installing /Users/bamcgill/work/sandbox/dbtools-commons/hudsonplugin/pom.xml to /tmp/m2/oracle/dbtools/hudsonplugin/1.0-SNAPSHOT/hudsonplugin-1.0-SNAPSHOT.pom [INFO] Installing /Users/bamcgill/work/sandbox/dbtools-commons/hudsonplugin/target/hudsonplugin.jar to /tmp/m2/oracle/dbtools/hudsonplugin/1.0-SNAPSHOT/hudsonplugin-1.0-SNAPSHOT.jar [INFO] ------------------------------------------------------------------------ [INFO] Reactor Summary: [INFO]  [INFO] DBTools Resource Generation maven plugin ........... SUCCESS [ 27.255 s] [INFO] DBTools Common Project Parent POM .................. SUCCESS [  9.551 s] [INFO] DBTools Common Library ............................. SUCCESS [ 22.922 s] [INFO] DBTools HTTP Library ............................... SUCCESS [  0.599 s] [INFO] DBTools REST JDBC Driver ........................... SUCCESS [  3.432 s] [INFO] DBTools SQLDeveloper SQLcl Library and Distribution  SUCCESS [ 16.765 s] [INFO] DBTools SQLcl Plugin for Hudson .................... SUCCESS [06:03 min] [INFO] ------------------------------------------------------------------------ [INFO] BUILD SUCCESS [INFO] ------------------------------------------------------------------------ [INFO] Total time: 17:21 min [INFO] Finished at: 2018-04-12T14:31:59+01:00 [INFO] Final Memory: 68M/1270M [INFO] ------------------------------------------------------------------------ ``` |

  
You can compare yours to the [complete log](https://gist.github.com/bamcgill/ddc34ba4ff8e283c8bb8407c2105a2b7) I dropped up on GitHub as a gist
