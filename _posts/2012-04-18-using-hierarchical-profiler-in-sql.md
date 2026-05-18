---
title: "Using Hierarchical Profiler in SQL Developer"
date: 2012-04-18 13:30:00 +0000
last_modified_at: 2012-04-19 07:50:46 +0000
tags:
  - hierarchial profiler
  - SQLDEVELOPER
---

One of the features exposed since SQL Developer 1.5 is the hierarchical profiler.  There have been several blogs and things about this but none I think that really get into the detail of what you are seeing and how to do it.  
  
The hierarchical profiler allows you to see what happens when your piece of PL/SQL is running.  More specifically, it allows you to see where it is spending most of its time, which means you can concentrate on hammering that down, rather than wondering where to start.  
  
For today, I'm using a really basic reference table with a few rows in it to allow us to do something.  I have also created two procedures, one of which calls the other so we have some nested dependencies.  
  

```
drop table hier_demo;
create table hier_demo (id number, name varchar2(200));
insert into hier_demo values (1, 'Barry');
insert into hier_demo values (2, 'Lisa');
insert into hier_demo values (3, 'Rebecca');
insert into hier_demo values (4, 'Katie-Ellen');

CREATE OR REPLACE
PROCEDURE PRINTER(
    NAME IN VARCHAR2 )
AS
BEGIN
  dbms_output.put_line(NAME);
END PRINTER;
/
CREATE OR REPLACE
PROCEDURE SHOW_PEEPS
AS
  CURSOR hiercur
  IS
    SELECT * FROM hier_demo;
  -- hierrec hiercur%type;
  -- type  hiertab is table of hierrec%TYPE;
BEGIN
  FOR myrec IN hiercur
  LOOP
    dbms_output.put_line(myrec.name);
  END LOOP;
END;
/
```

  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgqsoMrc2flh0bdeNyLjXgje-aLnwUWD5uYyUJ6eFRWQyjPd08tuVtgMrUnBXMMSbXG9mGhJKJ4SOUbDusywpTZAMNP2crQcMgN4ZfebET9KnYeLWfAZ1qz1nfZFhbvZZiPHDcq5EMCJjY/s1600/Screen+Shot+2012-04-18+at+16.50.05.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgqsoMrc2flh0bdeNyLjXgje-aLnwUWD5uYyUJ6eFRWQyjPd08tuVtgMrUnBXMMSbXG9mGhJKJ4SOUbDusywpTZAMNP2crQcMgN4ZfebET9KnYeLWfAZ1qz1nfZFhbvZZiPHDcq5EMCJjY/s1600/Screen+Shot+2012-04-18+at+16.50.05.png)Running the main procedure normally gives us some nice and simple out put.  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgTf12XJfMtXNahXYH3IsUrsodxCVPM-7LExDgZzKDUtx_4qgNlgtr0QfWq7Xec2Y9xgexEVfKGa-XM6JkX3hVDQS4aCJLfIeNrWn4n_iqJTMyRM_QS1x_hhEEt_I2bpuAe7B6R-ZBGQuA/s1600/Screen+Shot+2012-04-18+at+16.50.49.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgTf12XJfMtXNahXYH3IsUrsodxCVPM-7LExDgZzKDUtx_4qgNlgtr0QfWq7Xec2Y9xgexEVfKGa-XM6JkX3hVDQS4aCJLfIeNrWn4n_iqJTMyRM_QS1x_hhEEt_I2bpuAe7B6R-ZBGQuA/s1600/Screen+Shot+2012-04-18+at+16.50.49.png)  
  
When we click on the profile button in the plsql editor, SQL Developer will check that you have the proper permissions and the associated table to use the profiler.   
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEipWcEAFlLS9Ovi0pIRQNo1HaR2E-YhDL-8HT6h3z0qBw0UOJAHM1FOVeiK3LgyAWuv9Epf46EPH8RROM0boSFg_0lBwVHiw8afCgDVPBrvW1bMxGRIAZLFNeR6W2I-K9RCyfFdONTd1Ks/s1600/Screen+Shot+2012-04-18+at+16.49.55.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEipWcEAFlLS9Ovi0pIRQNo1HaR2E-YhDL-8HT6h3z0qBw0UOJAHM1FOVeiK3LgyAWuv9Epf46EPH8RROM0boSFg_0lBwVHiw8afCgDVPBrvW1bMxGRIAZLFNeR6W2I-K9RCyfFdONTd1Ks/s1600/Screen+Shot+2012-04-18+at+16.49.55.png)

When you hit the profiler button , it first comes up with the run dialog to set the parameters for the stored procedure.  Hitting ok on this diualog will run the stored procedure and any issues it has will also pop up while you are profiling.

As this happens, the profiler  first checks to see if the there is a profiler log directory.  and if there is not one, it will prompt you to create one and get the appropriate permissions.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjV1BjJk3iO4_V9O2S2EUxUEAmj3NMbswus2BqI5VgS3b7svFWgWQk4PlYjY4TEL3cHXe4Grdwx7LtmCI_THjlHJUNSK170RYwa2o1qP8IkE4jmkX2Qr5BSv2cXhGXkey4ehb5tf2jHYUA/s320/Screen+Shot+2012-04-18+at+16.42.02.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjV1BjJk3iO4_V9O2S2EUxUEAmj3NMbswus2BqI5VgS3b7svFWgWQk4PlYjY4TEL3cHXe4Grdwx7LtmCI_THjlHJUNSK170RYwa2o1qP8IkE4jmkX2Qr5BSv2cXhGXkey4ehb5tf2jHYUA/s1600/Screen+Shot+2012-04-18+at+16.42.02.png)

Hitting ok on this makes the tool then set up the directory for the profile.  To do this, it needs to run some SQL as sys to do it.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiY1ZIRsXHBnckQ6VIDUgTjELzZieyinbXGWr6fCX5BIkR9g32LhBBEIn0iqPMmeBvzSD99LRoDL7f2xprpui8C_D-uqTZDIZt3P9f1bxSQjCyQR3zLN6wObh0r4ljghsk5ELQqa2dA7D8/s320/Screen+Shot+2012-04-18+at+14.57.48.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiY1ZIRsXHBnckQ6VIDUgTjELzZieyinbXGWr6fCX5BIkR9g32LhBBEIn0iqPMmeBvzSD99LRoDL7f2xprpui8C_D-uqTZDIZt3P9f1bxSQjCyQR3zLN6wObh0r4ljghsk5ELQqa2dA7D8/s1600/Screen+Shot+2012-04-18+at+14.57.48.png)

  
If the user agrees with all this, then he is prompted for SYS passwd to actually create the tables for the profiler statistics in the local user, in this case, hrdemo.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjTM47MDWFbvo_N5hKVgp1pUAOMKugXc3gL_g9Oybk5fzonFdfV6naJjsyc6R_kjSt4u6tBoIuUW8mprDbwGLAIuRxJINRhNcFU59qlMqcjUGSfrX1J3zgitKYwPiRuy5ItfWigpHU8x3U/s320/Screen+Shot+2012-04-18+at+16.42.23.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjTM47MDWFbvo_N5hKVgp1pUAOMKugXc3gL_g9Oybk5fzonFdfV6naJjsyc6R_kjSt4u6tBoIuUW8mprDbwGLAIuRxJINRhNcFU59qlMqcjUGSfrX1J3zgitKYwPiRuy5ItfWigpHU8x3U/s1600/Screen+Shot+2012-04-18+at+16.42.23.png)Finally, when they agree, the tool asks if it can setup a local set of tables for the profiler,  We'll agree to this too and make sure the profile is captured.

 Now, when we look at the profile tab of the PLSQL editor, we should have a new editor with the results of the profile.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjm54X8NQl5nsDEanxl30u7IBJLTAyHi3jkul5fdOiWqoSMsqCwJnbedwtWxY2WPOpTld0TiwKGUd_G0gGjNxkHs4_iCJxxEL1cLNxFiK9d12GrUz3_aifH6H00dmpP90GEZrT84cMfchM/s640/Screen+Shot+2012-04-18+at+17.21.09.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjm54X8NQl5nsDEanxl30u7IBJLTAyHi3jkul5fdOiWqoSMsqCwJnbedwtWxY2WPOpTld0TiwKGUd_G0gGjNxkHs4_iCJxxEL1cLNxFiK9d12GrUz3_aifH6H00dmpP90GEZrT84cMfchM/s1600/Screen+Shot+2012-04-18+at+17.21.09.png)

  
This shows us a breakdown of the how the procedure actually executed all the way down to the actual fetch which returned the rows.  A very slight change to the procedure, in this case adding another procedure as a dependency which we also described above, we can show the nesting in the profile going further down.  

```
create or replace
PROCEDURE SHOW_PEEPS
AS
  CURSOR hiercur
  IS
    SELECT * FROM hier_demo;
  -- hierrec hiercur%type;
  -- type  hiertab is table of hierrec%TYPE;
Begin
  FOR myrec IN hiercur
  Loop
    PRINTER(myrec.name);
  END LOOP;
END;
```

  
This now shows us that we have another profile in the set and clicking on it gives us the hierarchy of calls in the stored procedures execution.  The main point here is that we can now see the further level of indirection through the printer procedure.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2Kx05gmMQ63hVAcv_u4ImoRUK1oM9pH4kf6k_saps0S3mZvTrTfu2stFbb-T_KvPax2w-h0RN-jcAYJiU6SrqosdBoOKwMllJdJCJSl1f5nFMUK42cgkkLIZOJ5GPz8Xk2bMYpolVPHo/s640/Screen+Shot+2012-04-18+at+17.21.58.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2Kx05gmMQ63hVAcv_u4ImoRUK1oM9pH4kf6k_saps0S3mZvTrTfu2stFbb-T_KvPax2w-h0RN-jcAYJiU6SrqosdBoOKwMllJdJCJSl1f5nFMUK42cgkkLIZOJ5GPz8Xk2bMYpolVPHo/s1600/Screen+Shot+2012-04-18+at+17.21.58.png)

  
So thats all of this profiler for now,  If you want to see how to do this with your own tables, the easiest thing to do is to download the [Oracle Developer Days VM](http://www.oracle.com/technetwork/community/developer-vm/index.html) from [OTN](http://otn.oracle.com/).  This particular blog will make an appearance as part of a bigger set later which we will discuss Tuning in general..
