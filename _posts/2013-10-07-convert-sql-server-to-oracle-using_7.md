---
title: "Convert SQL Server to Oracle using files - Part 2"
date: 2013-10-07 22:47:00 +0000
last_modified_at: 2013-10-07 22:47:30 +0000
tags:
  - Convert
  - Translate
  - Offline Capture
  - SQLServer
  - SQL Developer
---

Ok, Now we have the files as generated and moved in [part 1](http://barrymcgillin.blogspot.co.uk/2013/10/convert-sql-server-to-oracle-using.html), we can now start SQL Developer to load the files. Start up SQL Developer  and create a connection with the following privileges: CONNECT, RESOURCE and CREATE VIEW.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiooNJXQMh8D2kMMtKJT3bFx66II8Q-7Y6JbpcJ3wGN8rND16r0WoEM12gvQBBOt4vZL0XNRjF-HlX1i1YDRkwsNHVGS_Ten-jVwZyBNuFZRorxesTcB5V7Y0hfjNHHgtzYpTLPXz4qNu0/s1600/Screen+Shot+2013-10-07+at+22.15.48.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiooNJXQMh8D2kMMtKJT3bFx66II8Q-7Y6JbpcJ3wGN8rND16r0WoEM12gvQBBOt4vZL0XNRjF-HlX1i1YDRkwsNHVGS_Ten-jVwZyBNuFZRorxesTcB5V7Y0hfjNHHgtzYpTLPXz4qNu0/s1600/Screen+Shot+2013-10-07+at+22.15.48.png)

When the connection is opened, right click on it and choose Migration Repository then Associate Migration Repository.  This will create the repository in the connection.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhvAc5zilqtoAfBP3y5GsQrMyy-nDoOHQrUC_C6cu57UT2pD8tOBQ9T9Mlee_eHKoWIETEale0nW9dKNEp96UgjpAg15cIEWbppygDnE6uAKP4UajGXqSE8QL_HwK_tCXn2U6uQEvU6jVA/s1600/Screen+Shot+2013-10-07+at+22.16.20.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhvAc5zilqtoAfBP3y5GsQrMyy-nDoOHQrUC_C6cu57UT2pD8tOBQ9T9Mlee_eHKoWIETEale0nW9dKNEp96UgjpAg15cIEWbppygDnE6uAKP4UajGXqSE8QL_HwK_tCXn2U6uQEvU6jVA/s1600/Screen+Shot+2013-10-07+at+22.16.20.png)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjAAkQXZoYB9LztZ4cvPEicSo84AHvZnh0f9WoT3Zo3B7Gp3-ik9Sou3Gj47V-mtq8m4k-jEPwm3SvCqnszNEGdTg2X5MhurZUvuw0v0C9I5R_XslwczNMiHc-LpjE8Li8rD1AsaInMFNM/s1600/Screen+Shot+2013-10-07+at+22.17.08.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjAAkQXZoYB9LztZ4cvPEicSo84AHvZnh0f9WoT3Zo3B7Gp3-ik9Sou3Gj47V-mtq8m4k-jEPwm3SvCqnszNEGdTg2X5MhurZUvuw0v0C9I5R_XslwczNMiHc-LpjE8Li8rD1AsaInMFNM/s1600/Screen+Shot+2013-10-07+at+22.17.08.png)

 Now, We can start the migration wizard. You can do this by either going to the tools menu and selecting migrate from the migration menu, or you can select the migrate icon from the migration project navigator.  The wizard will popup and you can walk through the steps as outlined below.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgcIthTQ4yZ0myWj10vBrBFyjpF3FdnEiih_9_OsLRBci5XKCZkR3vIHEPhhC5w_KmYqLta5qId9jT0_nuajMI9pcGVMK-dBwKrlm_7OSCw1gCGLHr70fXzlt5m-6MDcZUpb9zBfB3Ml3s/s1600/Screen+Shot+2013-10-07+at+22.18.13.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgcIthTQ4yZ0myWj10vBrBFyjpF3FdnEiih_9_OsLRBci5XKCZkR3vIHEPhhC5w_KmYqLta5qId9jT0_nuajMI9pcGVMK-dBwKrlm_7OSCw1gCGLHr70fXzlt5m-6MDcZUpb9zBfB3Ml3s/s1600/Screen+Shot+2013-10-07+at+22.18.13.png)

 Clicking the next button selects the repository page which we can choose the repository connection we just made.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEieQa0fbmCWrWZepV-6bwKefTvXEE8jdXIcpCU5wOB-ZZ-lIFW2Mh0s1IT9l8IdDyjBvwJZlglT90_6CKjmbxD2MTuic32H2YVCqxQ1YP3mIvHPEg5oiIWG531jw7E7lLAcN0TDgVyPsZo/s1600/Screen+Shot+2013-10-07+at+22.18.26.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEieQa0fbmCWrWZepV-6bwKefTvXEE8jdXIcpCU5wOB-ZZ-lIFW2Mh0s1IT9l8IdDyjBvwJZlglT90_6CKjmbxD2MTuic32H2YVCqxQ1YP3mIvHPEg5oiIWG531jw7E7lLAcN0TDgVyPsZo/s1600/Screen+Shot+2013-10-07+at+22.18.26.png)

 Next page and we need to create a project to hold the captured databases.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjHzdaBs7o6Q5oGk-u4rbbMCjeJJ48akAJQ_W3uwbMW3dvY-h3MrioTtb9Pcbsn1bu5a7M-0CE2f0BSnS4VVWEZvOhskhGoRrSimkahs9DenDyhjFEYc6JN20ena_GPAbCJxQOX9bJLXjY/s1600/Screen+Shot+2013-10-07+at+22.34.20.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjHzdaBs7o6Q5oGk-u4rbbMCjeJJ48akAJQ_W3uwbMW3dvY-h3MrioTtb9Pcbsn1bu5a7M-0CE2f0BSnS4VVWEZvOhskhGoRrSimkahs9DenDyhjFEYc6JN20ena_GPAbCJxQOX9bJLXjY/s1600/Screen+Shot+2013-10-07+at+22.34.20.png)

The output directory in the page above is the directory where any log files or generated files will be placed.  When we generate DDL or data move files, this is where they will get generated.  Next page is the capture page.  For using the files from Part 1, we need to choose offline which will then show the page below, which asks us to select the offline capture file.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgIC8JWPrPYO8nHjQs1SU6J6ZCdgOuyy5e_lNnzNAdRZPfVPW2GhW9cbd0RKEQfULc3Nx4p-CgZ6Qdj0Uh-t2Bj26bZ8Tc_-NefWRlDi47JThYjEZiHID9cNLsXcjnxGsx0mpiX-1U0qGk/s1600/Screen+Shot+2013-10-07+at+22.35.09.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgIC8JWPrPYO8nHjQs1SU6J6ZCdgOuyy5e_lNnzNAdRZPfVPW2GhW9cbd0RKEQfULc3Nx4p-CgZ6Qdj0Uh-t2Bj26bZ8Tc_-NefWRlDi47JThYjEZiHID9cNLsXcjnxGsx0mpiX-1U0qGk/s1600/Screen+Shot+2013-10-07+at+22.35.09.png)

 This offline capture file is in the zip file we brought over from SQL Server.  Browse to the sqlserver2008.ocp.  This file tells SQL Developer what to expect in the directory.  It will look for the databases that have been unloaded.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhc_fNk3V8ZhhCvQzzwxfJHtj4_8krNIuMTsbu0lQ65mORwXZV1bxnWWzJPwI22qgpw3f7RStx4PZ0JhCydAbb_KlSJuhZ89NNNLndjvgIsYu0gmDvmh0zIOZFu2eBLShdTwEhFmMoPyyg/s1600/Screen+Shot+2013-10-07+at+22.34.55.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhc_fNk3V8ZhhCvQzzwxfJHtj4_8krNIuMTsbu0lQ65mORwXZV1bxnWWzJPwI22qgpw3f7RStx4PZ0JhCydAbb_KlSJuhZ89NNNLndjvgIsYu0gmDvmh0zIOZFu2eBLShdTwEhFmMoPyyg/s1600/Screen+Shot+2013-10-07+at+22.34.55.png)

 When its selected, SQL Developer parses the files and shows you a list of the databases you ran the offline capture scripts for in Part 1.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEist0VfZBGbeJ69EKqYaY5HQU3G5GjXx8uvMbmQfd7FMSXX-xBXwPrzWgs0eFaDT_jx9p83gRsoPZdg9k-wgHPdv_6GKQng4rPGVVYoTGxP1giagcLdA0EnyIAsLNZbFts5BxYowrIfkjk/s1600/Screen+Shot+2013-10-07+at+22.35.22.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEist0VfZBGbeJ69EKqYaY5HQU3G5GjXx8uvMbmQfd7FMSXX-xBXwPrzWgs0eFaDT_jx9p83gRsoPZdg9k-wgHPdv_6GKQng4rPGVVYoTGxP1giagcLdA0EnyIAsLNZbFts5BxYowrIfkjk/s1600/Screen+Shot+2013-10-07+at+22.35.22.png)

 Choose both databases and click next.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEisIWj7fCSPQJqL6e5jcOeFZEamKITIulH_Rny1myLuoBeggclG_MS8Brlom7iDH0P7CyHipEmcsDqwX0o5BQll7pR8VPmzOYCNhOZP93YSYECb38u5VpjjUddUC3lChWHAZ4niJhz0iH8/s1600/Screen+Shot+2013-10-07+at+22.35.34.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEisIWj7fCSPQJqL6e5jcOeFZEamKITIulH_Rny1myLuoBeggclG_MS8Brlom7iDH0P7CyHipEmcsDqwX0o5BQll7pR8VPmzOYCNhOZP93YSYECb38u5VpjjUddUC3lChWHAZ4niJhz0iH8/s1600/Screen+Shot+2013-10-07+at+22.35.34.png)

 The next page shows a list of the datatypes of SQL Server on the left and a list of equivalent data types on the right.  You can choose a different type if you want and you can also create a new mapping by clicking on the "Add new Rule".  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiV0l3AGqZdi8mmYkwBZFfIGnAWTMUVW4vVulQk7TXpTFJ1deF2h6LIFgU65eOrGAi2CQCJZKkL8F8jG7-_-L5i69TWOhy-4HFO4eOMyki04EolsuKNaxivHrH1QQ01MLt3JH3YTFpoXr0/s1600/Screen+Shot+2013-10-07+at+22.35.50.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiV0l3AGqZdi8mmYkwBZFfIGnAWTMUVW4vVulQk7TXpTFJ1deF2h6LIFgU65eOrGAi2CQCJZKkL8F8jG7-_-L5i69TWOhy-4HFO4eOMyki04EolsuKNaxivHrH1QQ01MLt3JH3YTFpoXr0/s1600/Screen+Shot+2013-10-07+at+22.35.50.png)

 The next page lists the objects to be translated.  Because we have not captured anything yet, the best we can do is to tell SQL Developer to translate everything.  We can come back later and choose specific  stored programs to convert and translate.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEieoIJZafvkPW-rKkZxtyJzLEjv_R17JaeKot4BqCjHTZoKdleDR3i-05LDmYKN9Tqfxw1QvxlWBIG9CFl2TeVg2PGwAp9G_qgk4PCOv2cBPIxyRvR4FOQmDcl2Zrij845MSx9wN4zL4xE/s1600/Screen+Shot+2013-10-07+at+22.36.49.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEieoIJZafvkPW-rKkZxtyJzLEjv_R17JaeKot4BqCjHTZoKdleDR3i-05LDmYKN9Tqfxw1QvxlWBIG9CFl2TeVg2PGwAp9G_qgk4PCOv2cBPIxyRvR4FOQmDcl2Zrij845MSx9wN4zL4xE/s1600/Screen+Shot+2013-10-07+at+22.36.49.png)

 At this stage, we can click proceed to summary and then finish once you review the summary page.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhu64GjMNJ6I4s_heG09kzsvWnONpCgsuGAdNJaj8gRdWY2cweoX71oFp1-NNVOAgkY8a0bkpkVPg2ncWOAUlMeY7yidryZdC5hHO-Ls-A1_xCFbbbA1juvCIW0MYPa3CNcmR8AdAbTWnY/s1600/Screen+Shot+2013-10-07+at+22.37.06.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhu64GjMNJ6I4s_heG09kzsvWnONpCgsuGAdNJaj8gRdWY2cweoX71oFp1-NNVOAgkY8a0bkpkVPg2ncWOAUlMeY7yidryZdC5hHO-Ls-A1_xCFbbbA1juvCIW0MYPa3CNcmR8AdAbTWnY/s1600/Screen+Shot+2013-10-07+at+22.37.06.png)

 When finish is pressed, SQL Developer will capture the database metadata from the files and convert it to its Oracle equivalent.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXMTYhwGeH_ZoWtbEpuSyO-JI-m0AuSg2UlXgBTRM9plqtbt8nRV84u4VLlmtLVXGGFa9sxBCtHL19eoqhKsDCXmrIapbtD6H6uvZdDMHbOs7lOXn3oF_YImpD74HjF7WFw0NBPv4Nj9w/s1600/Screen+Shot+2013-10-07+at+22.37.20.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXMTYhwGeH_ZoWtbEpuSyO-JI-m0AuSg2UlXgBTRM9plqtbt8nRV84u4VLlmtLVXGGFa9sxBCtHL19eoqhKsDCXmrIapbtD6H6uvZdDMHbOs7lOXn3oF_YImpD74HjF7WFw0NBPv4Nj9w/s1600/Screen+Shot+2013-10-07+at+22.37.20.png)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_gAjDkTGPgbvdxHklMWG18LdZaPtkz611J3FJc7RTcLFFHd9G7L3KhaIm8VotGpd-KgBqluXiYpX5CnB-ryqSU8pqH3YRfyN1vKnzD4MCBYqOl7eArPzMQTAVMYbdcmiEPl9mUBn_-8U/s1600/Screen+Shot+2013-10-07+at+22.37.55.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_gAjDkTGPgbvdxHklMWG18LdZaPtkz611J3FJc7RTcLFFHd9G7L3KhaIm8VotGpd-KgBqluXiYpX5CnB-ryqSU8pqH3YRfyN1vKnzD4MCBYqOl7eArPzMQTAVMYbdcmiEPl9mUBn_-8U/s1600/Screen+Shot+2013-10-07+at+22.37.55.png)

 When this completes, you will see a new node with the project name you chose earlier. If you click on it, you will get an editor on the right hand side with a summary of the data captured and converted.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUiBArvkrWUxIcSDTRwFCTKY1Bax5osnmTXR-uNhsD7afEnzbC1h_mideILRClR-Ug59ecnig7NfvPlTVnAHhruNLpmt0jTW1JJ7YY2jmRGPevGbXesqxIbHJq48VshUreZYx7Xb1FttU/s1600/Screen+Shot+2013-10-07+at+22.38.56.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUiBArvkrWUxIcSDTRwFCTKY1Bax5osnmTXR-uNhsD7afEnzbC1h_mideILRClR-Ug59ecnig7NfvPlTVnAHhruNLpmt0jTW1JJ7YY2jmRGPevGbXesqxIbHJq48VshUreZYx7Xb1FttU/s1600/Screen+Shot+2013-10-07+at+22.38.56.png)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCmuvmqmOg8PT8ct7R91s-rY_mSGy6WIQLtg2oj9XdCSJ3kzNSi39ciUBL-XqrShn2PZFfraB705QhYk37Nen4TL5WHo_W6byn6VsC3hygM-4S6EQnptbLdjIASKkS5ZmK_7rNvN417g8/s1600/Screen+Shot+2013-10-07+at+22.41.00.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCmuvmqmOg8PT8ct7R91s-rY_mSGy6WIQLtg2oj9XdCSJ3kzNSi39ciUBL-XqrShn2PZFfraB705QhYk37Nen4TL5WHo_W6byn6VsC3hygM-4S6EQnptbLdjIASKkS5ZmK_7rNvN417g8/s1600/Screen+Shot+2013-10-07+at+22.41.00.png)
