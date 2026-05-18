---
title: "SQL Developer Data Pump Support - Part 2"
date: 2011-09-12 17:17:00 +0000
last_modified_at: 2011-09-12 17:17:53 +0000
tags:
  - oracle
  - import
  - Data pump
  - SQL Developer
  - 11g
---

Welcome to part 2 of this feature on our introduction of data pump functionality into [SQL Developer](http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html).  [Previously](http://barrymcgillin.blogspot.com/2011/09/sql-developer-data-pump-support-part-1.html), we walked through exporting from the database.  This post will go through the importing the data export to a new schema in our database.  
In the DBA navigator, go to the data pump node, and choose 'Data Pump Import Wizard'.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh1CTuxwEknst7_X-9MHfplaHJT5B-93QBpxJ7msDDP4p1SnsNFLmLAd5qROpFBZwW5KRzv9ZX0P3U2YaKLrZ6KkGiojibauYeIzFLG_NvfpKrsxMeXkbLo7ud7AfuV5PmjkRLKWhIzK-M/s1600/import_menu.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh1CTuxwEknst7_X-9MHfplaHJT5B-93QBpxJ7msDDP4p1SnsNFLmLAd5qROpFBZwW5KRzv9ZX0P3U2YaKLrZ6KkGiojibauYeIzFLG_NvfpKrsxMeXkbLo7ud7AfuV5PmjkRLKWhIzK-M/s1600/import_menu.PNG)

When the wizard appears, choose the type of import you want.   In our previous episode, we exported the 'BARRY' Schema.  We'll now choose to do a schema import.

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVTdXLUW2Ep2ETUfkpu_k3BNIOHczC2kJNE8mR7tNn6S39UFQRy7d7IItK9QcqrYKSK7PVEPUvv20da6EnzUwjKXvhcU6X4nwUGiERWTi12Dj5EZOovouNcKhWZg2goMGCXFmauJ_bJuM/s320/import_wizard1.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVTdXLUW2Ep2ETUfkpu_k3BNIOHczC2kJNE8mR7tNn6S39UFQRy7d7IItK9QcqrYKSK7PVEPUvv20da6EnzUwjKXvhcU6X4nwUGiERWTi12Dj5EZOovouNcKhWZg2goMGCXFmauJ_bJuM/s1600/import_wizard1.PNG)

For the input directories, choose a directory that exists and you have access to.  The dump files from the export session need to reside on this directory and conform to the filename as specified.  
Hitting next, will parse the files and step 2 shows us the available schema to choose from.  Since we only export 'BARRY', we only have one to choose from in this case.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiv_tTQ-N3lT7d9cWmB6x9owpMx5QMnr1oysVoKSkWAc12KVflppU5GgMvQ4K1UhPa8lmy5KtrJFUPdFfOmg5lclpAoQP4k84Jy-JlGxHjD5cqfURntDu3xGfthZQ25t7_HrFMF6r0iR80/s320/import_wizard2.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiv_tTQ-N3lT7d9cWmB6x9owpMx5QMnr1oysVoKSkWAc12KVflppU5GgMvQ4K1UhPa8lmy5KtrJFUPdFfOmg5lclpAoQP4k84Jy-JlGxHjD5cqfURntDu3xGfthZQ25t7_HrFMF6r0iR80/s1600/import_wizard2.PNG)

Step 3 involves remapping.  In this case, on my database, the Barry schema exists.  I need to create another schema to create these objects in.  I've done this already before we started the wizard.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvSELGlWtVMUP7lah9T1skldp-2DZrPhLkA3llJ8lqU8veB_1BSyd2EytJwrdx2gWI1eGQ4WsFHv3GEF4k4jPr0TS9KBul1scYn-oTMmY9DzQHQVeWJ7vbx0HF873i7PY-PJVOsBj7Nag/s320/create+new+schema.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvSELGlWtVMUP7lah9T1skldp-2DZrPhLkA3llJ8lqU8veB_1BSyd2EytJwrdx2gWI1eGQ4WsFHv3GEF4k4jPr0TS9KBul1scYn-oTMmY9DzQHQVeWJ7vbx0HF873i7PY-PJVOsBj7Nag/s1600/create+new+schema.PNG)

Once the schema has been created and we're back in the wizard, we can set the destination as 'BARRY2'

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgmyAb8OUznjjnk-azidRREt_HbfEa2dApJjniUo8GafTKSmURZy5D04OK3x4FJWf1-ATe3E7KpzJl06JeqPf0Vev0wEqGotSPln2N0O5VsizrTSCFESJEAZYZoOJUB3P7WESPw6UsZs0Q/s320/import_wizard3.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgmyAb8OUznjjnk-azidRREt_HbfEa2dApJjniUo8GafTKSmURZy5D04OK3x4FJWf1-ATe3E7KpzJl06JeqPf0Vev0wEqGotSPln2N0O5VsizrTSCFESJEAZYZoOJUB3P7WESPw6UsZs0Q/s1600/import_wizard3.PNG)  

Step 4 has two parts, one is for logging and we choose an appropriate database directory for that which exists and we have access to.  The second is for the actions on tables if they exist.  In my case, I want to replace them.  For this example, we know its a fresh schema with nothing in it, but if it did, we'd be replacing the tables.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRvzK6GK8Mln7GRRrC1oLIQSVuw7mAnP2Pdmz4ojbb_RWyBPKzFjY2ZgY1L3gj8lBX7VwDrOcsRnT_l_XoYpAKeE_X5eHAu8PlueBGCre2PO-X05Xl-ggH0SZcv0wTztcblvU9u6HrsLA/s320/import_wizard4.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRvzK6GK8Mln7GRRrC1oLIQSVuw7mAnP2Pdmz4ojbb_RWyBPKzFjY2ZgY1L3gj8lBX7VwDrOcsRnT_l_XoYpAKeE_X5eHAu8PlueBGCre2PO-X05Xl-ggH0SZcv0wTztcblvU9u6HrsLA/s1600/import_wizard4.PNG)  

Lastly, we can schedule the import, and like last time, I want to do this immediately.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhqM7AfwBFeMDMseq78EvRuv_VTkEV8H_4aNyfZn9O7mf02KblZw48euaNQnVPKeyjMlFPBdbHXA08cjl65HdNh-Rfc21E21H8f5M-fonopU46kn3wUZdnTRszzNDXF5snqPaZ41Dm7tsI/s320/import_wizard5.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhqM7AfwBFeMDMseq78EvRuv_VTkEV8H_4aNyfZn9O7mf02KblZw48euaNQnVPKeyjMlFPBdbHXA08cjl65HdNh-Rfc21E21H8f5M-fonopU46kn3wUZdnTRszzNDXF5snqPaZ41Dm7tsI/s1600/import_wizard5.PNG)  

The summary shows us what will be done on our behalf and once we hit the finish button, an import job will be created and kicked off immediately.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhln_5Aql-34HrfEKOMDQGecewTJaReGE6AcUVwonfLCFlJ0zs84a66eDnI0F5_VPneON8t9T-4hEVNkQottPBR8vDhXrF0DT6cHzCwfoSvVI5TYMKDC46Z4lFenf1jxMcfCDS1Rf-Wi_s/s320/import_wizard6.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhln_5Aql-34HrfEKOMDQGecewTJaReGE6AcUVwonfLCFlJ0zs84a66eDnI0F5_VPneON8t9T-4hEVNkQottPBR8vDhXrF0DT6cHzCwfoSvVI5TYMKDC46Z4lFenf1jxMcfCDS1Rf-Wi_s/s1600/import_wizard6.PNG)  
  

When the job starts, there will be an import job shown in the dba navigator.  its corresponding editor will show the job executing.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjWRVPSW35vhDIRK1kYIJVWXeTPPbtOLzWwXMh7gh9IwKPt69PNaEejJmOOjxqyqu6b7jcCxqdVilqjrW53J9aMSHNDOqOquid6kz-Zi9lEIuB_DWXIcOf3ofE68Zlo9uaPrdbPznn8Qo8/s1600/import_status.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjWRVPSW35vhDIRK1kYIJVWXeTPPbtOLzWwXMh7gh9IwKPt69PNaEejJmOOjxqyqu6b7jcCxqdVilqjrW53J9aMSHNDOqOquid6kz-Zi9lEIuB_DWXIcOf3ofE68Zlo9uaPrdbPznn8Qo8/s1600/import_status.PNG)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEioG57tTuNaEr_TU8MuK0bC0dUIJlriNKP49stpfdiyKOHwrQvV66_xbb9L5sd7jGxRsPP9gFi3anisWQcS2NDEzk6Aodmi7qNoOUc0OnysPUVqOrqkXqnwPn2NbL5ZjnzPwNiFiMWYmAw/s320/import_status2.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEioG57tTuNaEr_TU8MuK0bC0dUIJlriNKP49stpfdiyKOHwrQvV66_xbb9L5sd7jGxRsPP9gFi3anisWQcS2NDEzk6Aodmi7qNoOUc0OnysPUVqOrqkXqnwPn2NbL5ZjnzPwNiFiMWYmAw/s1600/import_status2.PNG)

Finally, we can create a connection for the BARRY2 schema and look at the data.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj-a51X4aU1mQNxvFb3CoKLV2WRHSDsukb9TCez0kl8ePVrwONlDzASYgJb2vIcBj-BPNwAD2KLsdle0Jjna1xyZJXHVYrBQofj3iXKjhIOgxelW2k0vsIruQn-4WMHyb6RKdrqfH636xI/s320/new_barry2_conn.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj-a51X4aU1mQNxvFb3CoKLV2WRHSDsukb9TCez0kl8ePVrwONlDzASYgJb2vIcBj-BPNwAD2KLsdle0Jjna1xyZJXHVYrBQofj3iXKjhIOgxelW2k0vsIruQn-4WMHyb6RKdrqfH636xI/s1600/new_barry2_conn.PNG)  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhqysmmh9N0f99eocLa1NM8L13PIuSur6AOodZJAGiilZxE6VEz23j9ix0DibpFiHz2fAN06S7zTX2z_oOjPM2BwtaRCDWygSNny6SjqDJRvtZLxYcVgbugG24O5Jxn-GQWlkca8D9_ZDw/s320/imported_tables.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhqysmmh9N0f99eocLa1NM8L13PIuSur6AOodZJAGiilZxE6VEz23j9ix0DibpFiHz2fAN06S7zTX2z_oOjPM2BwtaRCDWygSNny6SjqDJRvtZLxYcVgbugG24O5Jxn-GQWlkca8D9_ZDw/s1600/imported_tables.PNG)

  
 So, that's it in a nutshell.  Over two parts, we've shown you how to export any part of a database to file using the data pump utilities which have been integrated into [Oracle SQL Developer](http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html).  In this part, we took those files from the previous post and imported them into Oracle.
