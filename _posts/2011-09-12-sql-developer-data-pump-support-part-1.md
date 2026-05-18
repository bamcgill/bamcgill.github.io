---
title: "SQL Developer Data Pump Support - Part 1"
date: 2011-09-12 16:20:00 +0000
last_modified_at: 2011-09-12 16:22:44 +0000
tags:
  - DBA
  - oracle
  - 11g
  - export
  - Data pump
  - SQL Developer
  - Oracle XE
---

In 3.1 we're adding support for Data Pump, which has replaced exp and imp.  In SQL Developer, we've added this in the DBA navigator which has support for several new things this release.  In this post, I'm only going through Data Pump export and in part 2 of this post, we'll visit the import.  We'll  revisit several of other new DBA features in the very near future.  For export, the demonstration will show that this is pretty easy to use, however, get a cup of coffee, cos we've a few snapshots to go through!

Ok, so first off, we need to fire up the DBA Navigator which can be reached from the view menu.  Select DBA and you get the navigator shown on the right. This image shows the sys user which has been selected as the current connection.  We're going to use the barry connection for using data pump today.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhbXdteOrHMuqA01tkn8-fU3D5hcKkauIuvNUzXBhqJ915zRGovAXnW76awXiviq_Xfo2x-o7VjkWAjY8rmXMveBp22ZphwroDvas9N9-7J9qvb2b2nSE1A47AbPrabtKqbYfJMlJgPRbk/s1600/menu.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhbXdteOrHMuqA01tkn8-fU3D5hcKkauIuvNUzXBhqJ915zRGovAXnW76awXiviq_Xfo2x-o7VjkWAjY8rmXMveBp22ZphwroDvas9N9-7J9qvb2b2nSE1A47AbPrabtKqbYfJMlJgPRbk/s1600/menu.PNG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgbJau8x6yWtvy24KXE7-tDBKT5Tngs8cY7aUCR9RFj66NBmiq6-HJVfxF8-tjGThpX2tWfTyJBnMF9IjA-0p4ZTnJMx1L0bbNCpiX_nj2eECzvzLO7EU4TR72BrP4X6-dqSMFeSSyZJsg/s1600/dbawindow.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgbJau8x6yWtvy24KXE7-tDBKT5Tngs8cY7aUCR9RFj66NBmiq6-HJVfxF8-tjGThpX2tWfTyJBnMF9IjA-0p4ZTnJMx1L0bbNCpiX_nj2eECzvzLO7EU4TR72BrP4X6-dqSMFeSSyZJsg/s1600/dbawindow.PNG)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiDIjTXrrS5aqMk6Zm7eS0X565djm8hBYV3ggsNvXPo7mY0xupZm1UFIUdKrhONW8HUYd2984SyKdVOOOFBp-cSXHSq7g-ZvcQHLnpLmGUlSJzunRYzoYosLtP1AXv3fWvm0cwV4PtjIxw/s1600/dpexportmenu.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiDIjTXrrS5aqMk6Zm7eS0X565djm8hBYV3ggsNvXPo7mY0xupZm1UFIUdKrhONW8HUYd2984SyKdVOOOFBp-cSXHSq7g-ZvcQHLnpLmGUlSJzunRYzoYosLtP1AXv3fWvm0cwV4PtjIxw/s1600/dpexportmenu.PNG)

From the data pump node, select the menu item for the Data Pump Export Wizard.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiKsmm17lwM_na6NFNSy7gVcVTWvinnBW37yTU0a-tzWyyiH-ZRwlwHqpsOWfRTq2dlp5Yt0EWpWgu30gGxDwuDz8IgoZPAaNCJEWeXakfx-_ou_gUL33mW8S1ACZJld4Cz1dYLqDuLiko/s320/dpwiz1.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiKsmm17lwM_na6NFNSy7gVcVTWvinnBW37yTU0a-tzWyyiH-ZRwlwHqpsOWfRTq2dlp5Yt0EWpWgu30gGxDwuDz8IgoZPAaNCJEWeXakfx-_ou_gUL33mW8S1ACZJld4Cz1dYLqDuLiko/s1600/dpwiz1.PNG)

  

On the first page of this wizard, we are choosing schema today.  You also have the option of exporting the entire database, some tablespaces or a block of tables.  When you're ready press next

  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjTxcsv4NHHZK527VI7DseQ8haAHvSdhu8USnc7F_NyeclkKF07LJrx8cnt7_RYkzWWCVT15CDNRjF6goWvHet4UpO7RDUPaZaFnTIqNvlVzi9QutRMjDvOK_7hN1VKrCO8XL9E50a1mXM/s320/dpwiz2.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjTxcsv4NHHZK527VI7DseQ8haAHvSdhu8USnc7F_NyeclkKF07LJrx8cnt7_RYkzWWCVT15CDNRjF6goWvHet4UpO7RDUPaZaFnTIqNvlVzi9QutRMjDvOK_7hN1VKrCO8XL9E50a1mXM/s1600/dpwiz2.PNG)

  
  
As we said earlier, we are only choosing schema today and in the image below, we are only selecting one schema for export. The 'BARRY' schema.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi4Prxt8T9FMEViyQBc08vTj21ovVLP5PRwVwDxU6gnd69F4cM6NAwVxyEtEcxobqStNY0jL4fbPE4mcy41tEkBzkYZTl80stFzXoJA4dGp9RgRw8gX0IzsfB07RyURxKz7IgGmuKbcWHA/s320/dpwiz3.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi4Prxt8T9FMEViyQBc08vTj21ovVLP5PRwVwDxU6gnd69F4cM6NAwVxyEtEcxobqStNY0jL4fbPE4mcy41tEkBzkYZTl80stFzXoJA4dGp9RgRw8gX0IzsfB07RyURxKz7IgGmuKbcWHA/s1600/dpwiz3.PNG)

Step 3 allows you to filter what is exported by including or excluding various things, you can choose none of these things or, a  selection of each with an appropriate filter string in the value field.  
We won't add any today and let it take everything out of the schema.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQ1Yb_ztbC5tuBAnjK4WFojbmN8pyk8ebCcjDpR3s9WuaTqB1qTW9HqE3NwV-nCuofSqmjzLBOaZiUOnEt4MOuifm6djfRtQGOe1MAouSWUUvmdpFNmOPzqt9bKEqO-scgRlAsrpGwNAw/s320/dpwiz4.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQ1Yb_ztbC5tuBAnjK4WFojbmN8pyk8ebCcjDpR3s9WuaTqB1qTW9HqE3NwV-nCuofSqmjzLBOaZiUOnEt4MOuifm6djfRtQGOe1MAouSWUUvmdpFNmOPzqt9bKEqO-scgRlAsrpGwNAw/s1600/dpwiz4.PNG)

  
  
In Step 4, the data tab, we can add data filters to all the tables, or individual tables as required.  Again for this demonstration, I'm not going to choose any of that and let the data pump export everything.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgDTElC-uNeW0P2WMYaKCfjjwsX80R2FuyUmiRRJsmamdfZV2HQLmOqd6hgnl9Rnkrma2OmPTteKkgrIfXyKk9cOQgb2IQC67xyQQt2pQJnK5boS-SUa-0UKZinJ0tDOPBntww62ZGmRR4/s320/dpwiz5.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgDTElC-uNeW0P2WMYaKCfjjwsX80R2FuyUmiRRJsmamdfZV2HQLmOqd6hgnl9Rnkrma2OmPTteKkgrIfXyKk9cOQgb2IQC67xyQQt2pQJnK5boS-SUa-0UKZinJ0tDOPBntww62ZGmRR4/s1600/dpwiz5.PNG)

  
  
  
Step 5 allows us to specify the options for the export.  Our primary interest is in the directory for the  logging.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj00N8DZu2cnwJ_XjZz1NwReLDMKgK73-E7RileADx0n7q1Wk4PCJprhp1EpcVz8U1L4dv7rc1X7bv-CGafSBtI2Kpo4LaNyr1Jm6XC-b4FQnLAqWVvxlhQcr_Y2mf6_Mh3cI17rSThW4M/s320/dpwiz6.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj00N8DZu2cnwJ_XjZz1NwReLDMKgK73-E7RileADx0n7q1Wk4PCJprhp1EpcVz8U1L4dv7rc1X7bv-CGafSBtI2Kpo4LaNyr1Jm6XC-b4FQnLAqWVvxlhQcr_Y2mf6_Mh3cI17rSThW4M/s1600/dpwiz6.PNG)

  
Step 6 focuses on our Output directory.  Specify the one you want to use here.  Remember, as in Step 5, this directory must exist, and you must have the privileges to write to it from your user.  Check on the main connections navigator for directories.  By default there is a DATA\_PUMP\_DIR setup, but make sure that the directory exists.  We've created a directory called 'BARRYS\_DPUMP\_DIR' for this example.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEihpR1wH9kDGvGeNXhwysr5SK9h0dVEKMNknYZEjGj6OKb43WmBWabreTW7d8Z8rcWet07BjOhPfj98o1D1mSMLGZ1mUBkyFFWo2KgZ7NrtQjeIHWt0zC6DjLqtOiF-qIEspOWFlbvnUWA/s320/dpwiz7.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEihpR1wH9kDGvGeNXhwysr5SK9h0dVEKMNknYZEjGj6OKb43WmBWabreTW7d8Z8rcWet07BjOhPfj98o1D1mSMLGZ1mUBkyFFWo2KgZ7NrtQjeIHWt0zC6DjLqtOiF-qIEspOWFlbvnUWA/s1600/dpwiz7.PNG)  
  
  
  
Step 7 specifies the schedule which will dump the data for you.  We're choosing immediately as our option. You can specify whenever you like for this job to run, repeatedly if required.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhlDeLLTLEOcA4mwT0PaSr8dJmKaoSIiX7b8Uh1K0u9uaPFr20bOV65OjenBOQfajHETjdFTy8TvS7Xo0jtwlbRiQnVs1kb05LXQE0v19MRv-HLA22SAwEMs8hvKBtCjrnqQD_-TlpiZM0/s320/dpwiz8.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhlDeLLTLEOcA4mwT0PaSr8dJmKaoSIiX7b8Uh1K0u9uaPFr20bOV65OjenBOQfajHETjdFTy8TvS7Xo0jtwlbRiQnVs1kb05LXQE0v19MRv-HLA22SAwEMs8hvKBtCjrnqQD_-TlpiZM0/s1600/dpwiz8.PNG)  
  
Lastly, we have the summary screen, which is split in two parts. The main summary screen shows what actions you are taking and how they will be carried out.  The second panel shows the actual PL/SQL which will be run on your behalf to create the data pump job, and dump the data.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYsxq53mi4XKv_GNi6XvAZyV2iplkSZ5TpkThmPwF7TZLcYeQq4aBFZWuaKx0Hf2u8me1xEdsVE9obk-mXlUVK1eHpD-SOU067okpafS7rJjDSyp2OFK-0wPWfMmm4LyV4W69qV1j9hSs/s320/dpwiz9.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYsxq53mi4XKv_GNi6XvAZyV2iplkSZ5TpkThmPwF7TZLcYeQq4aBFZWuaKx0Hf2u8me1xEdsVE9obk-mXlUVK1eHpD-SOU067okpafS7rJjDSyp2OFK-0wPWfMmm4LyV4W69qV1j9hSs/s1600/dpwiz9.PNG)

When you click finish, and job submission is successful, you'll get  a new job listed in the DBA navigator under Data Pump export Jobs.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgHuoWDTWwVa16LZxd3tYjEpOBfDkDTflJ8aC2gBcKN2DKdvC4YUE9Rd5lZJD4yNcUudNtOh2V0BW-tw8t-qiRMv-2kwsWG5HR93AR63Ot1o_u6gQSktwf6xIcWaMROgYxOFsXN2QrEJkY/s320/job_status2.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgHuoWDTWwVa16LZxd3tYjEpOBfDkDTflJ8aC2gBcKN2DKdvC4YUE9Rd5lZJD4yNcUudNtOh2V0BW-tw8t-qiRMv-2kwsWG5HR93AR63Ot1o_u6gQSktwf6xIcWaMROgYxOFsXN2QrEJkY/s1600/job_status2.PNG)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiAdpq5khPV6XusOcBvPMcEHR8ESg8x1-PCjP7jMhUrh2tlxntWbBL36xdFuK_pF74NRp9LrPhzDjbVhLyps-zocFHG2NA7696hFFXUJwtjdmrCs63V1g6NwexBqi9uHR8xng1n453_sVc/s1600/job_status1.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiAdpq5khPV6XusOcBvPMcEHR8ESg8x1-PCjP7jMhUrh2tlxntWbBL36xdFuK_pF74NRp9LrPhzDjbVhLyps-zocFHG2NA7696hFFXUJwtjdmrCs63V1g6NwexBqi9uHR8xng1n453_sVc/s1600/job_status1.PNG)

  

If it doesn't appear, then it's highly likely you'll get this error, primarily due to the directory that you are writing the files or the logs to.  This is easily fixed by going back and making sure the directories you have chosen, exist and that you have access to read from and write to them.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEif8bN4SbalvGfmO57Nj-OoBnWBITxH01yI9q19zpVDFa5lu9G1PqDawn8X5zTuhDDNgZKTKN5gkkVT4YLAwoQDhD2Ye9wBtXiw1Y-Dv5OJ3YHf1leFrys3wH_WaSgexWq6qlXkFpGeiwo/s320/dp_dir_error.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEif8bN4SbalvGfmO57Nj-OoBnWBITxH01yI9q19zpVDFa5lu9G1PqDawn8X5zTuhDDNgZKTKN5gkkVT4YLAwoQDhD2Ye9wBtXiw1Y-Dv5OJ3YHf1leFrys3wH_WaSgexWq6qlXkFpGeiwo/s1600/dp_dir_error.PNG)

  
 Lastly, you can go to your database directory and see your exported file, together with the log file.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgMZwB-wjlpu_91xR-1f-3fvCEJeVxrTZzRw74y9FBw4a1rhNdgNoK_Y_DXuk6fRKlq4rcUtn9a4cKRGVhUeMiDLfGE7LNeLb9h0oEUoPlTz6SSfyaeAsECPgKfR9HniblVLGyEDunFp1M/s1600/dpwiz1.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgMZwB-wjlpu_91xR-1f-3fvCEJeVxrTZzRw74y9FBw4a1rhNdgNoK_Y_DXuk6fRKlq4rcUtn9a4cKRGVhUeMiDLfGE7LNeLb9h0oEUoPlTz6SSfyaeAsECPgKfR9HniblVLGyEDunFp1M/s1600/dpwiz1.PNG)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg1Kvc39ZJx1gHp9itU2HVi0iZuWG97LvHwcxqlF0T8zNxp1x1qW67MBdjs-SCdcSIOqa0PZt-T1l_z34Aigssz3y5OBT8T6V3ZpicUaIJjIaOFVQhbl-gniQ0VUEEsL1b0o64BP40hAyk/s320/job_done.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg1Kvc39ZJx1gHp9itU2HVi0iZuWG97LvHwcxqlF0T8zNxp1x1qW67MBdjs-SCdcSIOqa0PZt-T1l_z34Aigssz3y5OBT8T6V3ZpicUaIJjIaOFVQhbl-gniQ0VUEEsL1b0o64BP40hAyk/s1600/job_done.PNG)

  
  
 Your log file will contain something like this if you're successful. (I've cut a lot out of it as it is long)  
  

```
Starting "BARRY"."EXPORT_JOB_SQLDEV_327":  
Estimate in progress using BLOCKS method...
Processing object type SCHEMA_EXPORT/TABLE/TABLE_DATA
.  estimated "BARRY"."MD_ADDITIONAL_PROPERTIES"              3 MB
.  estimated "BARRY"."STAGE_TERADATA_TABLETEXT"          2.062 MB
.  estimated "BARRY"."MD_DERIVATIVES"                        2 MB
.  estimated "BARRY"."MD_FILE_ARTIFACTS"                     2 MB
...
.  estimated "BARRY"."文化大革命"                                 0 KB
Total estimation using BLOCKS method: 17.75 MB
Processing object type SCHEMA_EXPORT/USER
Processing object type SCHEMA_EXPORT/SYSTEM_GRANT
.....
Processing object type SCHEMA_EXPORT/TABLE/INDEX/STATISTICS/FUNCTIONAL_AND_BITMAP/INDEX_STATISTICS
Processing object type SCHEMA_EXPORT/TABLE/STATISTICS/TABLE_STATISTICS
. . exported "BARRY"."MD_ADDITIONAL_PROPERTIES"          13.54 KB      59 rows
. . exported "BARRY"."STAGE_TERADATA_TABLETEXT"          1.197 MB      25 rows
. . exported "BARRY"."MD_DERIVATIVES"                    49.60 KB     386 rows
...
. . exported "BARRY"."文化大革命"                                 0 KB       0 rows
Master table "BARRY"."EXPORT_JOB_SQLDEV_327" successfully loaded/unloaded
******************************************************************************
Dump file set for BARRY.EXPORT_JOB_SQLDEV_327 is:
  D:\DEMO\DPUMP\EXPDAT01.DMP
Job "BARRY"."EXPORT_JOB_SQLDEV_327" successfully completed at 15:42:52
```

  
So, for today, thats exporting from the Oracle database using the Datapump built into Oracle SQL Developer 3.1 which will be available soon!  We'll have part 2 on importing this dump file next.
