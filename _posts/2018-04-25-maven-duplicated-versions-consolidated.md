---
title: "Maven Duplicated Versions consolidated with flatten"
date: 2018-04-25 20:58:00 +0000
last_modified_at: 2018-04-25 20:58:24 +0000
tags:
  - flatten
  - maven
  - module
  - version
  - revision
---

We had the situation lately where we have a bunch of modules in a project and a common parent.  Now when we go to update the project version we need to update the parent version in EVERY pom.  
  
Lets take a look at a simple project  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhj4N6UmZ8F8rkEMz2oDkJRMZFxNPNljT2eVLeA7lML79XCV1PIzdwFmg_6HbkP1uoZE_sZlUL1dxw6gqo47Wa8BZjn7jT6iAUk7C2WZcLrGOYcb2ztZsC3OXBBZiC-XamHj6Mpd-AAcv4/s320/Screen+Shot+2018-04-25+at+19.41.06.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhj4N6UmZ8F8rkEMz2oDkJRMZFxNPNljT2eVLeA7lML79XCV1PIzdwFmg_6HbkP1uoZE_sZlUL1dxw6gqo47Wa8BZjn7jT6iAUk7C2WZcLrGOYcb2ztZsC3OXBBZiC-XamHj6Mpd-AAcv4/s1600/Screen+Shot+2018-04-25+at+19.41.06.png)

This project has three simple modules which have a common parent

```
1:  <project>  
3:      <modelVersion>4.0.0</modelVersion>  
4:      <packaging>pom</packaging>  
5:      <name>Three Stooges</name>  
6:      <groupId>oracle.blogger</groupId>  
7:      <artifactId>stooges</artifactId>  
8:      <version>1.0.0-SNAPSHOT</version>  
9:      <properties>  
10:          <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  
11:      </properties>  
12:      <modules>  
13:          <module>larry</module>  
14:          <module>curley</module>  
15:          <module>moe</module>  
16:      </modules>  
17:  </project>
```

Each module inherits from the parent including the version.  Lets take a look at Larrys module.  
  

```
1:  <project>  
3:      <modelVersion>4.0.0</modelVersion>  
4:      <packaging>jar</packaging>  
5:      <name>Larry</name>  
6:      <artifactId>larry</artifactId>  
7:      <parent>  
8:          <groupId>oracle.blogger</groupId>  
9:          <artifactId>stooges</artifactId>  
10:          <version>1.0.0-SNAPSHOT</version>  
11:      </parent>  
12:  </project>
```

  
In our larger project, we had over 20 of these to change at once when we branched for release  
  
Instead, we introduced a revision property in the parent pom, which was then used to be the version in all the pom's. Here's the modified parent pom with the revision in place.  
  

```
1:  <project>  
3:       <modelVersion>4.0.0</modelVersion>  
4:       <packaging>pom</packaging>  
5:       <name>Three Stooges</name>  
6:       <groupId>oracle.blogger</groupId>  
7:       <artifactId>stooges</artifactId>  
8:       <version>${revision}</version>  
9:       <properties>  
10:            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  
11:            <flatten.version>1.0.1</flatten.version>  
12:            <!-- Build Revision -->  
13:            <revision>1.0.1-SNAPSHOT</revision>  
14:       </properties>  
15:       <modules>  
16:            <module>larry</module>  
17:            <module>curley</module>  
18:            <module>moe</module>  
19:       </modules>
```

  
and in each of the children, that change propagates like this.  
  

```
1:  <project>  
2:       <modelVersion>4.0.0</modelVersion>  
3:       <packaging>jar</packaging>  
4:       <name>Larry</name>  
5:       <artifactId>larry</artifactId>  
6:       <parent>  
7:            <groupId>oracle.blogger</groupId>  
8:            <artifactId>stooges</artifactId>  
9:            <version>${revision}</version>  
10:       </parent>  
11:  </project>
```

  
Now, for most things, this all works and we can see that in the build.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQxnfumR89yCLXG1zWGaRGdu9eRM9IKTKZ7bFqtHQteBikJ7IRGCCKHVMtPHqsrYdCPYsJtQvSRMVF_vyCgtcBFZfI_D2UEmWvILZ68uI9vsy1hkiZJ-RN61TmOxttx038xe7yf-9_t4s/s400/Screen+Shot+2018-04-25+at+20.12.11.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQxnfumR89yCLXG1zWGaRGdu9eRM9IKTKZ7bFqtHQteBikJ7IRGCCKHVMtPHqsrYdCPYsJtQvSRMVF_vyCgtcBFZfI_D2UEmWvILZ68uI9vsy1hkiZJ-RN61TmOxttx038xe7yf-9_t4s/s1600/Screen+Shot+2018-04-25+at+20.12.11.png)

  
But, when we deploy these builds to artifactory, we need to flatten the poms with the versions so that they can be used for versioning.  We can use the [Maven Flatten Plugin](https://www.mojohaus.org/flatten-maven-plugin/) from [mojoHaus](https://www.mojohaus.org/) to help with this. What this does to the pom is:  
  
  
- Build specific elements are removed
- Development specific elements are removed by default
- It only contains elements required for users of your artifact
- Its variables are resolved
- Its parent relationship is resolved, flattened and removed
- Its build time driven profiles **can** be evaluated so their impact gets embedded
- JDK or OS driven profiles still remain allowing dynamic dependencies if needed
  
  
Add it to your parent pom pluginManagement section.  
  

```
1:       <build>  
2:            <pluginManagement>  
3:                 <plugins>  
4:                      <plugin>  
5:                           <groupId>org.codehaus.mojo</groupId>  
6:                           <artifactId>flatten-maven-plugin</artifactId>  
7:                           <version>${flatten.version}</version>  
8:                           <configuration>  
9:                                <updatePomFile>true</updatePomFile>  
10:                           </configuration>  
11:                           <executions>  
12:                                <execution>  
13:                                     <id>flatten</id>  
14:                                     <phase>process-resources</phase>  
15:                                     <goals>  
16:                                          <goal>flatten</goal>  
17:                                     </goals>  
18:                                </execution>  
19:                                <execution>  
20:                                     <id>flatten.clean</id>  
21:                                     <phase>clean</phase>  
22:                                     <goals>  
23:                                          <goal>clean</goal>  
24:                                     </goals>  
25:                                </execution>  
26:                           </executions>  
27:                      </plugin>  
28:                      <plugin>  
29:                           <groupId>org.eclipse.m2e</groupId>  
30:                           <artifactId>lifecycle-mapping</artifactId>  
31:                           <version>${lifecycle-mapping.version}</version>  
32:                           <configuration>  
33:                                <lifecycleMappingMetadata>  
34:                                     <pluginExecutions>  
35:                                          <pluginExecution>  
36:                                               <pluginExecutionFilter>  
37:                                                    <groupId>org.codehaus.mojo</groupId>  
38:                                                    <artifactId>flatten-maven-plugin</artifactId>  
39:                                                    <versionRange>[0,)</versionRange>  
40:                                                    <goals>  
41:                                                         <goal>flatten</goal>  
42:                                                    </goals>  
43:                                               </pluginExecutionFilter>  
44:                                               <action>  
45:                                                    <ignore></ignore>  
46:                                               </action>  
47:                                          </pluginExecution>  
48:                                     </pluginExecutions>  
49:                                </lifecycleMappingMetadata>  
50:                           </configuration>  
51:                      </plugin>  
52:                 </plugins>  
53:            </pluginManagement>  
54:            <plugins>  
55:                 <plugin>  
56:                      <groupId>org.codehaus.mojo</groupId>  
57:                      <artifactId>flatten-maven-plugin</artifactId>  
58:                 </plugin>  
59:            </plugins>  
60:       </build>
```

  
This will run as part of the build like this  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXh5kAh3WP4xxWzKS4qmKAgW1xMqBDULlhJUmFhHVqSAvv6toAKxLae9sIpPgnJHPaNWonpuupc2DMpwmgUjef72NewG_5la3UxpdRAvG7gxs9hi26k2YDSgI0mnZd6ik5Wl7IkDmgZE0/s400/Screen+Shot+2018-04-25+at+20.32.31.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXh5kAh3WP4xxWzKS4qmKAgW1xMqBDULlhJUmFhHVqSAvv6toAKxLae9sIpPgnJHPaNWonpuupc2DMpwmgUjef72NewG_5la3UxpdRAvG7gxs9hi26k2YDSgI0mnZd6ik5Wl7IkDmgZE0/s1600/Screen+Shot+2018-04-25+at+20.32.31.png)

  
and will produce a flattened pom for you  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHhXIWJ5eghSwsESEn-rfWvT3JlSnBQ49_Ge2N9F8LrtAzl-pNOd6sVAajtOnR6sowKwkh2zquUMq9UukiR2cmxpdWLMsbzaNgBiBq1mbubL7y6tvALHDyBd1srVrPBtvmOVnROFYKseE/s400/Screen+Shot+2018-04-25+at+20.34.35.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHhXIWJ5eghSwsESEn-rfWvT3JlSnBQ49_Ge2N9F8LrtAzl-pNOd6sVAajtOnR6sowKwkh2zquUMq9UukiR2cmxpdWLMsbzaNgBiBq1mbubL7y6tvALHDyBd1srVrPBtvmOVnROFYKseE/s1600/Screen+Shot+2018-04-25+at+20.34.35.png)

without all the variables and so on as detailed above.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiSl9Mg0R3EImOXwHOArQOkEHcVmr_eTfCjToAPBC9mh_7VZ2atgwMxpccgzHfiurQuUkB0QcdxmOHXdbUXcXww65-GdQNYYbGaQJqzxe2wvlJVUb5dNai9lGk2EehzVhYi7ZqYLnzJCOc/s400/Screen+Shot+2018-04-25+at+20.35.57.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiSl9Mg0R3EImOXwHOArQOkEHcVmr_eTfCjToAPBC9mh_7VZ2atgwMxpccgzHfiurQuUkB0QcdxmOHXdbUXcXww65-GdQNYYbGaQJqzxe2wvlJVUb5dNai9lGk2EehzVhYi7ZqYLnzJCOc/s1600/Screen+Shot+2018-04-25+at+20.35.57.png)

mvn clean will remove all created files afterwards to leave your original pom.xml.  The pull request in the repo looked like this before merge.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgs6YwJ9ruJEqpt02AapsSLine-NdEJVzHhnLIK047yHKJJ_kztIoxgHcW2p5DtXT6gvTvkhM1SaEp6nsEDuz8J3xinNdHY8SqDs_ZpdDVwmtXV3bu8qK_mUjRzfFo6YJSu3R1q6WlydUQ/s400/Screen+Shot+2018-04-25+at+20.49.45.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgs6YwJ9ruJEqpt02AapsSLine-NdEJVzHhnLIK047yHKJJ_kztIoxgHcW2p5DtXT6gvTvkhM1SaEp6nsEDuz8J3xinNdHY8SqDs_ZpdDVwmtXV3bu8qK_mUjRzfFo6YJSu3R1q6WlydUQ/s1600/Screen+Shot+2018-04-25+at+20.49.45.png)
