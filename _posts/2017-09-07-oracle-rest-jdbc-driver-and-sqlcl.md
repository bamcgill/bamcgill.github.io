---
title: "Oracle REST JDBC Driver and SQLcl"
date: 2017-09-07 14:09:00 +0000
last_modified_at: 2017-09-07 14:09:59 +0000
tags:
  - REST
  - jdbc
  - sqlcl
  - ORDS
---

Oracle just released its first REST JDBC driver on OTN, in conjunction with the 17.3.0 Oracle REST Data Services Beta release.  
  
[Dermot posted this morning](http://dermotoneill.blogspot.co.uk/2017/09/getting-started-with-rest-enabled-sql.html) about how to setup ORDS and Enable REST SQL Statements. The JDBC driver connects to this service and allows you to connect your JDBC based program to a REST services.  
  
As an example of this working with a standard application we can download the driver and drop it into Oracle SQLcl and connect to a service out of the box.  
  
  

- Firstly download [SQLcl from OTN](http://www.oracle.com/technetwork/developer-tools/sqlcl/downloads/index.html)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEifr-KyWp6Tcf3wLhiTs0boAHDhlf3ZtNnLwFmY1_9jsdWPnonKMx-pa4WHuIiwfMi3EDnR4Pzq_F-os-rL5xK7QdmraPJmwGepzqhNc2VpJFcP2uE2T-eM9ydt-WEA9b7vzUENHg2OVRY/s640/Screen+Shot+2017-09-07+at+11.52.29.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEifr-KyWp6Tcf3wLhiTs0boAHDhlf3ZtNnLwFmY1_9jsdWPnonKMx-pa4WHuIiwfMi3EDnR4Pzq_F-os-rL5xK7QdmraPJmwGepzqhNc2VpJFcP2uE2T-eM9ydt-WEA9b7vzUENHg2OVRY/s1600/Screen+Shot+2017-09-07+at+11.52.29.png)

- Unzip the sqlcl-17.2.0.184.1230-no-jre.zip

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVi65afTHrEkTHHj4XzcWx9JmsShjGIuzRE1Vbe3vH2vEXaQ3nfR9CB6oSUQZbJ8nsg8nemXO0_xKpwsKTEbGDsAibIuKriJtu9HQnkKpL38jiT_CsXKMjhvngqJdNv_kO3zX3awLTMlg/s640/Screen+Shot+2017-09-07+at+12.00.38.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVi65afTHrEkTHHj4XzcWx9JmsShjGIuzRE1Vbe3vH2vEXaQ3nfR9CB6oSUQZbJ8nsg8nemXO0_xKpwsKTEbGDsAibIuKriJtu9HQnkKpL38jiT_CsXKMjhvngqJdNv_kO3zX3awLTMlg/s1600/Screen+Shot+2017-09-07+at+12.00.38.png)

- Download the [JDBC Beta Driver from OTN](http://www.oracle.com/technetwork/developer-tools/rest-data-services/downloads/ords-beta-173-3873522.html)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhwm2ICpP9UcCcicood606hMiOh90ECi-FsLGKW2RgXNp6yWmRM9aYtKF8iSlmgic9ZKAfF1cZGmmVGsndYWYPW0sf8s21CnHi6HZuyC0PqEJ7lDWlnR_v5atNo7RAHakO4jG6w31CgKxk/s640/Screen+Shot+2017-09-07+at+11.39.59.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhwm2ICpP9UcCcicood606hMiOh90ECi-FsLGKW2RgXNp6yWmRM9aYtKF8iSlmgic9ZKAfF1cZGmmVGsndYWYPW0sf8s21CnHi6HZuyC0PqEJ7lDWlnR_v5atNo7RAHakO4jG6w31CgKxk/s1600/Screen+Shot+2017-09-07+at+11.39.59.png)

  

- and drop it into the SQLcl lib directory

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjJZIV80gyNWODNnbgu_GbxSR0Fo3JuV_ywqsR50nUfjBiwNHjoMEKL7QdkKwi4uRtJELGgLUWEefsgtbr5Zt-dJqFAdShQvMH9WtQKM-W1fde7ja4yiA417wHB-cMDBv4qbUQTJO4XbPQ/s640/Screen+Shot+2017-09-07+at+15.00.43.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjJZIV80gyNWODNnbgu_GbxSR0Fo3JuV_ywqsR50nUfjBiwNHjoMEKL7QdkKwi4uRtJELGgLUWEefsgtbr5Zt-dJqFAdShQvMH9WtQKM-W1fde7ja4yiA417wHB-cMDBv4qbUQTJO4XbPQ/s1600/Screen+Shot+2017-09-07+at+15.00.43.png)

- Lastly start sqlcl with your appropriate URL, in my case is demo/demo@http:///ords//

  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLeWwWRqfHhtvNpzQaPFKb25CDeHWqRhlQyRL3IeK757VAF7ruSEwcMMFSjmIq-srNQf15XRWkXIn-Rbpx5ZzncAR3EsQJhB8M48cHc1e6y_J72xOZ02QZZxEiqx2cTJWZoG1AMK1i_UI/s640/Screen+Shot+2017-09-07+at+12.35.54.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLeWwWRqfHhtvNpzQaPFKb25CDeHWqRhlQyRL3IeK757VAF7ruSEwcMMFSjmIq-srNQf15XRWkXIn-Rbpx5ZzncAR3EsQJhB8M48cHc1e6y_J72xOZ02QZZxEiqx2cTJWZoG1AMK1i_UI/s1600/Screen+Shot+2017-09-07+at+12.35.54.png)
