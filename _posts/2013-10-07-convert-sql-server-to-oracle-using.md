---
title: "Convert SQL Server to Oracle using files - Part 1"
date: 2013-10-07 21:45:00 +0000
last_modified_at: 2013-10-07 21:45:28 +0000
tags:
  - offline
  - SQL Server
  - scripts
  - Migration
  - database migration
---

Many people want to migrate their SQL Server databases and do not have direct network access to the database. In Oracle SQL Developer, we can migrate from SQL Developer to Oracle using a connection  to SQL Server or  using files to extract the metadata from SQL Server and convert it to an Oracle equivilent.  
  
Today, we'll show you how to use scripts to convert SQL Server.  First we need to start up SQL Developer and choose the Tools menu, then select Migration and Create Offline Capture Scripts  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQUN1qBaiI3dik9UW2EsVhfkixf6ZKte8-DAPw7usP_IyITtPNbesfrTfglNrJlz_s0o8Tz90VkTtoiE0tncjdqtdVsFe9-FCdunsP4Hyig231dNlynwShGARekiZC7XazqxTDEMDThFw/s1600/Screen+Shot+2013-10-07+at+17.55.06.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQUN1qBaiI3dik9UW2EsVhfkixf6ZKte8-DAPw7usP_IyITtPNbesfrTfglNrJlz_s0o8Tz90VkTtoiE0tncjdqtdVsFe9-FCdunsP4Hyig231dNlynwShGARekiZC7XazqxTDEMDThFw/s1600/Screen+Shot+2013-10-07+at+17.55.06.png)

  
When the dialog appears, choose the SQL Server and the appropriate version you want.  You will also need to choose a directory to put the scripts into.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiEImbkws-IVUdkFuGEQ59DLKC8JSdNVHwZxQC5kh7wrGfGtw_LzkzBu15MXXRrbvJhazrchixbxYQGsdePVgpWQ_9ARejPQ8e0GfkgSndx78TUnSW_IkuqFIv9tJRQ77ZL3w40SiTiZwg/s1600/Screen+Shot+2013-10-07+at+17.59.31.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiEImbkws-IVUdkFuGEQ59DLKC8JSdNVHwZxQC5kh7wrGfGtw_LzkzBu15MXXRrbvJhazrchixbxYQGsdePVgpWQ_9ARejPQ8e0GfkgSndx78TUnSW_IkuqFIv9tJRQ77ZL3w40SiTiZwg/s1600/Screen+Shot+2013-10-07+at+17.59.31.png)

This will generate a set of files which we will need to move to our SQL Server machine to run.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_JFaIQ6O-NkDdg3jdxcwM_UiFub2WSp7Dxl4fLXRSjxA4erl2nZNOyQx9nfwIpVN7jZyGuibYv415j9z09ONpQE_TsSRve_PE29q-nUZX6ZmJE7LXqA1rC3E02yrw0FD8icKf_AyYjhQ/s1600/Screen+Shot+2013-10-07+at+18.00.36.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_JFaIQ6O-NkDdg3jdxcwM_UiFub2WSp7Dxl4fLXRSjxA4erl2nZNOyQx9nfwIpVN7jZyGuibYv415j9z09ONpQE_TsSRve_PE29q-nUZX6ZmJE7LXqA1rC3E02yrw0FD8icKf_AyYjhQ/s1600/Screen+Shot+2013-10-07+at+18.00.36.png)

So on disk, these look like this.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhfA3FJXnfxD617zx13ks2mhVVsQCvXzVUNL9t15r-GFJ-RpmBxJWKx2Z5xffpo3NP7cjU36gFGvdDgPb_toFaETFdpClZXzQ5Rp6cq30ba07Vrbj8Xruogdcgy2Ty0bk8FZWCxXuRi5d4/s1600/Screen+Shot+2013-10-07+at+18.06.56.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhfA3FJXnfxD617zx13ks2mhVVsQCvXzVUNL9t15r-GFJ-RpmBxJWKx2Z5xffpo3NP7cjU36gFGvdDgPb_toFaETFdpClZXzQ5Rp6cq30ba07Vrbj8Xruogdcgy2Ty0bk8FZWCxXuRi5d4/s1600/Screen+Shot+2013-10-07+at+18.06.56.png)

Now, we can zip this up and ftp it to the SQL Server machine you want to migrate, or in my case, I'll scp it to the machine.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQL7T3g9h5Q_IRm3ZZ1wfoLQafbGb2ftE6TfIFy7Fjtt8fWfNauAxjr9Srp8m5GclvINs94MsMoQYXfCnssx16bXOL_1LLasI0qTT9uXxiBlTk8JP1Nh5kEqsDnTJ1ZBMLpScVLVjKYqI/s1600/Screen+Shot+2013-10-07+at+18.11.12.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQL7T3g9h5Q_IRm3ZZ1wfoLQafbGb2ftE6TfIFy7Fjtt8fWfNauAxjr9Srp8m5GclvINs94MsMoQYXfCnssx16bXOL_1LLasI0qTT9uXxiBlTk8JP1Nh5kEqsDnTJ1ZBMLpScVLVjKYqI/s1600/Screen+Shot+2013-10-07+at+18.11.12.png)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiLIMhipVH6iRDcvSo19WaiFMmdMp0bsNtBYaX3H25o13JcbffE6mqpdzcrOc-30LEOq30VifWbKrA3CAGL2qEddz8Wb309NDX9Wv4C7pycYSgnmROmPukMiNxRIvY3ERLgoJ4KzCXmhFc/s1600/Screen+Shot+2013-10-07+at+18.15.42.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiLIMhipVH6iRDcvSo19WaiFMmdMp0bsNtBYaX3H25o13JcbffE6mqpdzcrOc-30LEOq30VifWbKrA3CAGL2qEddz8Wb309NDX9Wv4C7pycYSgnmROmPukMiNxRIvY3ERLgoJ4KzCXmhFc/s1600/Screen+Shot+2013-10-07+at+18.15.42.png)

Now, lets go to SQL Server and run the scripts against the SQL Server database.  Looking below, I have opened up a command window and created a directory called blog and moved the sqlserver.zip file into that directory.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiAmXcvfniLlklPrR5up-2RTr5IlbjiD4eQm4VKiVsFfByYVoxxsmRcBHcPEYVEHvIRxiLGx9FvbrUwHPUyBiGZAlFQHkEtW0N9Wf1qFGpMGMlRBNTjZMHaam-TD5Fl8xiURrYyPU3AlFo/s1600/Screen+Shot+2013-10-07+at+18.39.08.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiAmXcvfniLlklPrR5up-2RTr5IlbjiD4eQm4VKiVsFfByYVoxxsmRcBHcPEYVEHvIRxiLGx9FvbrUwHPUyBiGZAlFQHkEtW0N9Wf1qFGpMGMlRBNTjZMHaam-TD5Fl8xiURrYyPU3AlFo/s1600/Screen+Shot+2013-10-07+at+18.39.08.png)

Now, we have the scripts on the SQL Server box and ready to run.  Its important that when you run the scripts on a server, that you always run it from the same place.  The script which is run takes a number of parameters to run.

```
```
OMWB_OFFLINE_CAPTURE sa superuser_password databasename server
```
```

  

```
  OMWB_OFFLINE_CAPTURE sa saPASSWORD DBNAME_TO_CAPTURE SQLSERVER_SERVER
```

  
This will unload the metadata from the database to flat files.  You need to run this script once for each database you want to migrate.  You'll see something like these as you go.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjlO0YUytExiD3jaR0lphLZWXMha0TbGSfbj8b4t9DqhShP6v2nCoZu6XEKyyhP1fFy-KFLMJh0mNz22sdEZ3Mfa5NrDHL6SF3TtlRe4aKa-OdyBli4Qg3mDVWnbS26w6jQTP5YpF2-bZI/s1600/Screen_Shot_2013-10-07_at_21.00.36.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjlO0YUytExiD3jaR0lphLZWXMha0TbGSfbj8b4t9DqhShP6v2nCoZu6XEKyyhP1fFy-KFLMJh0mNz22sdEZ3Mfa5NrDHL6SF3TtlRe4aKa-OdyBli4Qg3mDVWnbS26w6jQTP5YpF2-bZI/s1600/Screen_Shot_2013-10-07_at_21.00.36.png)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCrd-fdXjomlIjgBt839QPMmMNlu2ns_5Xk3GAtPsKf8FpLQDgQEKTQNadCf7lqDJVej-yb5ZC9sqSMrRSkF3sk8LvI7cHm-dxii7yGecsImFGBiO_TNmwKEYzBLklQyExfEAXfExkEWw/s1600/Screen+Shot+2013-10-07+at+21.03.50.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCrd-fdXjomlIjgBt839QPMmMNlu2ns_5Xk3GAtPsKf8FpLQDgQEKTQNadCf7lqDJVej-yb5ZC9sqSMrRSkF3sk8LvI7cHm-dxii7yGecsImFGBiO_TNmwKEYzBLklQyExfEAXfExkEWw/s1600/Screen+Shot+2013-10-07+at+21.03.50.png)

This is one run for the northwind database.  I've run this again for the pubs database and lets look and see what files exist now.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhvpJq5b5rXse_k-mda4mCizlgIu8_Ix2RQ_Dk-o3ikUs-7sQdT8uxPe8DP7hjdZomRpd7SaWWohrfejc47v-5StgtgoIlNg4otrwd_AaVmWJnbaPt9k8vGB7QP_GR_4vByFvh-ltD2Q68/s1600/Screen+Shot+2013-10-07+at+21.21.24.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhvpJq5b5rXse_k-mda4mCizlgIu8_Ix2RQ_Dk-o3ikUs-7sQdT8uxPe8DP7hjdZomRpd7SaWWohrfejc47v-5StgtgoIlNg4otrwd_AaVmWJnbaPt9k8vGB7QP_GR_4vByFvh-ltD2Q68/s1600/Screen+Shot+2013-10-07+at+21.21.24.png)

Now, we go up a directory and zip all this up so we can move it to the machine where we will translate it.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg-cRe0Yp4434Md_llI5IcH-nKJgtMUSo3XgLLnpVFXbTH5M94YTwE9JTGqipecSRE1O4uOG4cu9Gc9Cuhp_cDMwz8iVU1eB1jcyY17gKKxvsN9HCLiImGt90DmjBzg-IFL07UEEI5Coq4/s1600/Screen+Shot+2013-10-07+at+21.43.44.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg-cRe0Yp4434Md_llI5IcH-nKJgtMUSo3XgLLnpVFXbTH5M94YTwE9JTGqipecSRE1O4uOG4cu9Gc9Cuhp_cDMwz8iVU1eB1jcyY17gKKxvsN9HCLiImGt90DmjBzg-IFL07UEEI5Coq4/s1600/Screen+Shot+2013-10-07+at+21.43.44.png)

Now, we can move that zip file.  Take a look at it, it is very small in size for this demo, but even for a large system, we are only capturing the metadata structure of the database.  If you are working with a partner or SI, this is the file you will want to send them for analysis.  
  
Ok, for those of you who are doing this right now, read on.  
  
When you have the capture.zip file transferred, unzip it into a clean directory.  We will use SQL Developer on this to  convert these metadata files into DDL to create the new Oracle schema and the data move scripts which can be used to unload the data from SQL Server and load it into Oracle.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEib2FjGKFuSGQWcpnKaNdSG-k7Pic9eJX1EsJ85sg19myYmRaKSus3UrtG_i4qbmJlqJrzvB4Cu-Qg7khWXmRAbpR6h5DOV0cjqR7edM3oYcNdkRO1DqSxPxg1-Xrn0fmpcPqQdz22H9HA/s1600/Screen+Shot+2013-10-07+at+22.02.59.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEib2FjGKFuSGQWcpnKaNdSG-k7Pic9eJX1EsJ85sg19myYmRaKSus3UrtG_i4qbmJlqJrzvB4Cu-Qg7khWXmRAbpR6h5DOV0cjqR7edM3oYcNdkRO1DqSxPxg1-Xrn0fmpcPqQdz22H9HA/s1600/Screen+Shot+2013-10-07+at+22.02.59.png)

Now, we use SQL Developer to load this data.  We will need access to an Oracle database to create a schema to use as a repository. The repository is used to hold the source database information and the converted data.

The next post will walk through SQL Developer loading these files and converting the metadata to an Oracle equivalent.
