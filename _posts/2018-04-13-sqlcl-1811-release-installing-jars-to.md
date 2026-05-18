---
title: "SQLCL 18.1.1 Release installing jars to local maven repository"
date: 2018-04-13 11:28:00 +0000
last_modified_at: 2018-04-13 11:28:39 +0000
tags:
  - open source
  - oracle
  - maven
  - GitHub
  - SQLDEVELOPER
  - Database Tools
  - dbtools
  - sqlcl
---

Here we are again releasing Oracle SQLcl. We released Oracle SQLDeveloper SQLcl 18.1.1 yesterday with only one significant change.  
  
Why? Well, we haven't changed the SQLcl code in this release but we've made it easier for you to use the libraries we ship with it.  We've added a [pom.xml](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) into the lib directory.  On a day to day use of SQLcl, this will not affect your use of SQLcl, however, it will allow you to install the libraries we ship with SQLcl into your local [maven repository](https://maven.apache.org/guides/introduction/introduction-to-repositories.html).  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi9Y1m6aWu4dH-qkqhj-0nFrxAPBwjhYOCHINvLtN8OsvQRiY26ukBwdbPziOjvDo2Iz5YRa00kHYoZJS9yKmL7bAo_OOjnKHng_GGn3BKshnvtc-mxRmrEGH06Pl35Fdc4VLZfysIVve0/s400/Screen+Shot+2018-04-13+at+10.15.58.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi9Y1m6aWu4dH-qkqhj-0nFrxAPBwjhYOCHINvLtN8OsvQRiY26ukBwdbPziOjvDo2Iz5YRa00kHYoZJS9yKmL7bAo_OOjnKHng_GGn3BKshnvtc-mxRmrEGH06Pl35Fdc4VLZfysIVve0/s1600/Screen+Shot+2018-04-13+at+10.15.58.png)

  
  
How does that work?  Well, you need to have [maven](http://maven.apache.org/download.cgi) installed in order to run the install.  You can check you have it like this.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjdkRpMuaXDXwiL_IkfDeYcDX_Azi7Ky7U-Lfv745XD5jWFumAheiY_Ina_qI-7fBv1FMI2DEbKy8NL19VeHXakE6QBq_4Wk197glOCA0rg_-e_v3I5PCYfg4CeIHX8U1r8PQ2kpRm2kOw/s400/Screen+Shot+2018-04-13+at+10.20.02.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjdkRpMuaXDXwiL_IkfDeYcDX_Azi7Ky7U-Lfv745XD5jWFumAheiY_Ina_qI-7fBv1FMI2DEbKy8NL19VeHXakE6QBq_4Wk197glOCA0rg_-e_v3I5PCYfg4CeIHX8U1r8PQ2kpRm2kOw/s1600/Screen+Shot+2018-04-13+at+10.20.02.png)

  
With confirmed you can run the install by invoking the command 'mvn validate' in the sqlcl/lib directory.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEheYopcx8_vWfBKogkNfM5Eg3tWyeKjKf0WHcAc_85sR_l6crEYbSkWexAFYK2TfLy9Q6rqA7QWiLDLy6JnaYO3fxiXYvKvq0dyy8pv-zqKKCD043QZPDg2HTWVvUu3PTHmcEFKO-G-dnc/s400/Screen+Shot+2018-04-13+at+11.24.57.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEheYopcx8_vWfBKogkNfM5Eg3tWyeKjKf0WHcAc_85sR_l6crEYbSkWexAFYK2TfLy9Q6rqA7QWiLDLy6JnaYO3fxiXYvKvq0dyy8pv-zqKKCD043QZPDg2HTWVvUu3PTHmcEFKO-G-dnc/s1600/Screen+Shot+2018-04-13+at+11.24.57.png)

which will take each jar and install it into your local maven repository.  By default, this will be ~/.m2

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgula69JepYAW1TALrcPSN7g1PziVKsUnxi5xsAaXb0Og_LN3P6a3PoijvWk92PQXdQCocyDKjk12BAPnV4KXfBe74B04skswiQjXjbPUKRCMR2zRWV1AAyelorK-9FuAdd8OtECdzS7P8/s400/Screen+Shot+2018-04-13+at+11.48.05.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgula69JepYAW1TALrcPSN7g1PziVKsUnxi5xsAaXb0Og_LN3P6a3PoijvWk92PQXdQCocyDKjk12BAPnV4KXfBe74B04skswiQjXjbPUKRCMR2zRWV1AAyelorK-9FuAdd8OtECdzS7P8/s1600/Screen+Shot+2018-04-13+at+11.48.05.png)

While a lot of these jars are available in maven.oracle.com and maven.org, there are several that aren't.  We're working on getting our production jars published externally.  The ones we dont have published publicly yet are:  
  

low-level-api.jar                  ojdbc8.jar

dbtools-common.jar                 oraclepki.jar

dbtools-http.jar                   orai18n-mapping.jar

dbtools-net.jar                    orai18n-utility.jar

dbtools-sqlcl.jar                  orai18n.jar

orajsoda.jar                       httpcore.jar

osdt\_cert.jar                      osdt\_core.jar

ucp.jar.                           jdbcrest.jar

xdb6.jar                           xmlparserv2-sans-jaxp-services.jar

  
if you want to add these to your project, take the following dependency management and prune it for your needs.   
  

```
1:      <dependencyManagement>  
2:          <dependencies>  
3:              <dependency>  
4:                  <groupId>com.oracle.jdbc</groupId>  
5:                  <artifactId>ojdbc8</artifactId>  
6:                  <version>12.2.0.1</version>  
7:              </dependency>  
8:              <dependency>  
9:                  <groupId>oracle.soda</groupId>  
10:                  <artifactId>orajsoda</artifactId>  
11:                  <version>12.2.0.1.0</version>  
12:              </dependency>  
18:              <dependency>  
19:                  <groupId>com.oracle.jdbc</groupId>  
20:                  <artifactId>xdb6</artifactId>  
21:                  <version>12.2.0.1</version>  
22:              </dependency>  
23:              <dependency>  
24:                  <groupId>com.oracle.jdbc</groupId>  
25:                  <artifactId>xmlparserv2-sans-jaxp-services</artifactId>  
26:                  <version>12.2.0.1</version>  
27:              </dependency>  
28:              <dependency>  
49:                  <groupId>com.oracle.jdbc</groupId>  
50:                  <artifactId>orai18n</artifactId>  
51:                  <version>12.2.0.1</version>  
52:              </dependency>  
53:              <dependency>  
54:                  <groupId>com.oracle.jdbc</groupId>  
55:                  <artifactId>orai18n-collation</artifactId>  
56:                  <version>12.2.0.1</version>  
57:              </dependency>  
58:              <dependency>  
59:                  <groupId>com.oracle.jdbc</groupId>  
60:                  <artifactId>orai18n-mapping</artifactId>  
61:                  <version>12.2.0.1</version>  
62:              </dependency>  
68:              <dependency>  
69:                  <groupId>com.oracle.jdbc</groupId>  
70:                  <artifactId>orai18n-utility</artifactId>  
71:                  <version>12.2.0.1</version>  
72:              </dependency>  
710:              <dependency>  
111:                  <groupId>oracle.dbtools</groupId>  
112:                  <artifactId>dbtools-common</artifactId>  
113:                  <version>18.1.1</version>  
114:              </dependency>  
115:              <dependency>  
116:                  <groupId>oracle.dbtools</groupId>  
117:                  <artifactId>dbtools-http</artifactId>  
118:                  <version>18.1.1</version>  
119:              </dependency>  
120:              <dependency>  
121:                  <groupId>oracle.dbtools</groupId>  
122:                  <artifactId>dbtools-sqlcl</artifactId>  
123:                  <version>18.1.1</version>  
124:              </dependency>  
125:              <dependency>  
126:                  <groupId>oracle.dbtools</groupId>  
127:                  <artifactId>jdbcrest</artifactId>  
128:                  <version>18.1.1</version>  
129:              </dependency>  
130:              <dependency>  
131:                  <groupId>com.oracle.jdbc</groupId>  
132:                  <artifactId>osdt_cert</artifactId>  
133:                  <version>12.2.0.1</version>  
134:              </dependency>  
135:              <dependency>  
136:                  <groupId>com.oracle.jdbc</groupId>  
137:                  <artifactId>osdt_core</artifactId>  
138:                  <version>12.2.0.1</version>  
139:              </dependency>  
140:              <dependency>  
141:                  <groupId>com.oracle.jdbc</groupId>  
142:                  <artifactId>oraclepki</artifactId>  
143:                  <version>12.2.0.1</version>  
144:              </dependency>  
160:              <dependency>  
161:                  <groupId>oracle.cloudstorage</groupId>  
162:                  <artifactId>low-level-api</artifactId>  
163:                  <version>13.0.0</version>  
164:              </dependency>  
170:          </dependencies>  
171:      </dependencyManagement>
```

  
Stay tuned, you'll have a project you can use this on soon!
