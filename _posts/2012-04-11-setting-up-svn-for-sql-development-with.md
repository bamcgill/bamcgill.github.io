---
title: "Setting up SVN for SQL Development with Oracle Developer Days VM"
date: 2012-04-11 20:41:00 +0000
last_modified_at: 2012-04-11 20:49:33 +0000
tags:
  - macosx
  - oracle
  - virtualbox
  - SQLDEVELOPER
  - Oracle Developer Day VM
  - SCM
---

We've done a number of posts on using the Oracle Developer Day VM's and this is an addition to it, showing how we can set up a subversion repository using apache web dav for access.    I'll keep this really simple so the steps should doable, straight one after the other.   
  
On the Oracle Developer Day image, we have installed SVN so we can use it as our source control system.  Lets find our svn.  

```
[oracle@localhost ~]$ which svn
/usr/bin/svn
[oracle@localhost ~]$
```

  
We can check if we have the right modules installed for apache, which in this case is mod\_dav\_svn.  

```
[oracle@localhost ~]$ ls /usr/lib/httpd/modules/|grep svn
[oracle@localhost ~]$
```

For this we need to make sure we have the proper SVN modules installed for apache.  We can do this with Yum. (The default repositories should be enough)  

```
[oracle@localhost /]$ sudo yum install mod_dav_svn
Loaded plugins: security
Setting up Install Process
Resolving Dependencies
There are unfinished transactions remaining. You might consider running yum-complete-transaction first to finish them.
The program yum-complete-transaction is found in the yum-utils package.
--> Running transaction check
---> Package mod_dav_svn.i386 0:1.6.11-7.el5_6.4 set to be updated
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package            Arch        Version                 Repository         Size
================================================================================
Installing:
 mod_dav_svn        i386        1.6.11-7.el5_6.4        el5_latest         78 k

Transaction Summary
================================================================================
Install       1 Package(s)
Upgrade       0 Package(s)

Total download size: 78 k
Is this ok [y/N]: y
Downloading Packages:
mod_dav_svn-1.6.11-7.el5_6.4.i386.rpm                    |  78 kB     00:00     
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing     : mod_dav_svn                                              1/1 

Installed:
  mod_dav_svn.i386 0:1.6.11-7.el5_6.4                                           

Complete!
[oracle@localhost /]$ cd /usr/lib/httpd/modules/
[oracle@localhost modules]$ ls *svn*
mod_authz_svn.so  mod_dav_svn.so
```

  
Now, we can create a repository somewhere to store some code which we'll save in here later.  I've added two repositories, just to show you can :).  
  

```
[oracle@localhost svn]$ svnadmin create /home/oracle/svn/repo1
[oracle@localhost svn]$ svnadmin create /home/oracle/svn/repo2
[oracle@localhost svn]$ ls repo1
conf  db  format  hooks  locks  README.txt
[oracle@localhost svn]$ cat repo1/README.txt 
This is a Subversion repository; use the 'svnadmin' tool to examine
it.  Do not add, delete, or modify files here unless you know how
to avoid corrupting the repository.

Visit http://subversion.tigris.org/ for more information.
[oracle@localhost svn]$
```

  
Now since we're going to access this over apache, lets change the permissions  

```
[oracle@localhost svn]$ sudo chown -R apache:apache /home/oracle/svn/repo1/
[sudo] password for oracle: 
[oracle@localhost svn]$ ls -al
total 16
drwxrwxr-x  3 oracle oracle 4096 Apr  9 21:53 .
drwxr-xr-x 45 oracle oracle 4096 Apr  9 21:51 ..
drwxrwxr-x  6 apache apache 4096 Apr  9 21:53 repo1
drwxrwxr-x  6 apache apache 4096 Apr  9 21:54 repo2
[oracle@localhost svn]$
```

We want to be able to secure svn, and for now, lets use basic svn authentication.  In order to do that, we need to configure subversion to allow users to connect.  To do that, go to your new repo, identify your svnserve.conf file and uncomment the following 2 lines  
  

```
auth-access = write
password-db = passwd
```

```
[oracle@localhost svn]$ cd repo1
[oracle@localhost repo1]$ ls
conf  db  format  hooks  locks  README.txt
[oracle@localhost repo1]$ cd conf/
[oracle@localhost conf]$ vi svnserve.conf 
[oracle@localhost conf]$ sudo vi svnserve.conf
```

  
Now setting up webdav for svn is relatively easy too.  Since we have the dav svn installed, we just need to edit the httpd.conf in /etc/httpd/conf/httpd.conf.   

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVVj1Qh7nvRniPxPT7y3v5xIclEkZzjHG2xkQpUd3Xh3SYRk7jYZTfVpWeRJGAF78_2ytngq1t_xoFnR1XpdvreYnXAa72191ON-pwako3eUnZ3qOQlWbrRUBuh0PMGf3K854Gjj_7fPU/s320/Screen+Shot+2012-04-11+at+19.14.31.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVVj1Qh7nvRniPxPT7y3v5xIclEkZzjHG2xkQpUd3Xh3SYRk7jYZTfVpWeRJGAF78_2ytngq1t_xoFnR1XpdvreYnXAa72191ON-pwako3eUnZ3qOQlWbrRUBuh0PMGf3K854Gjj_7fPU/s1600/Screen+Shot+2012-04-11+at+19.14.31.png)

The first we need to do is to modify the file and add the mod dav svn modules to apache.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhfYkRJg2oEEDnon_ca93mORhD5-LwpkekrlMHsMqs03LDa-rrIZaPIraxAZw8EqBf33x7xFUNGUr6eERUMKseezE9dG713iv9L6w74aIGkx6r97e_BkFEhRYSoELvJQ6k4GIG0YO7M7xc/s320/Screen+Shot+2012-04-11+at+19.15.11.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhfYkRJg2oEEDnon_ca93mORhD5-LwpkekrlMHsMqs03LDa-rrIZaPIraxAZw8EqBf33x7xFUNGUr6eERUMKseezE9dG713iv9L6w74aIGkx6r97e_BkFEhRYSoELvJQ6k4GIG0YO7M7xc/s1600/Screen+Shot+2012-04-11+at+19.15.11.png)

 In the same file, we also need to define a location for the our URLs to point to.    I have set this initial setup with the most basic setup which needs no authorization yet.  We'll amend that later.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiC3Y6U7aisyRFdFcfFpOB0kToYloap7HzckzGSSLj_eCnxvd72DSCSb0eNj2hOxzVgeBtEfKoX9ITCHG6MGetwH5-2H2UhmzmvSORZvfQUnuqP6L8xoq4MRyoAN-UlMjh9HlmPtIBcna0/s320/Screen+Shot+2012-04-11+at+19.15.57.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiC3Y6U7aisyRFdFcfFpOB0kToYloap7HzckzGSSLj_eCnxvd72DSCSb0eNj2hOxzVgeBtEfKoX9ITCHG6MGetwH5-2H2UhmzmvSORZvfQUnuqP6L8xoq4MRyoAN-UlMjh9HlmPtIBcna0/s1600/Screen+Shot+2012-04-11+at+19.15.57.png)

 Lastly, save the file, and we need to restart the httpd daemon.  This is in the /etc/init.d directory.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjaOPA4k3UeuQ1a3gAMlD_KFXHyhNB2-qJsZrqgUsf4EQr9-sutNTVfDW8cZBUvcpduyN9w9Oi_sWYFM5RDES5rkbm79WGOKFxURAVdgF9acB4ro4xtUZqkc_oNYlrSzOHqXK4ShJz8ZZ4/s320/Screen+Shot+2012-04-11+at+19.18.30.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjaOPA4k3UeuQ1a3gAMlD_KFXHyhNB2-qJsZrqgUsf4EQr9-sutNTVfDW8cZBUvcpduyN9w9Oi_sWYFM5RDES5rkbm79WGOKFxURAVdgF9acB4ro4xtUZqkc_oNYlrSzOHqXK4ShJz8ZZ4/s1600/Screen+Shot+2012-04-11+at+19.18.30.png)

 Now, we can check out if we can see this with a browser? Lets see.  We know that we set up the httpd.conf with a port number of 9999, so we can use the 'repos' location as the uri, and then we can specify the repository.  So, the url would be http://localhost:9999/repos/repo1 (or repo2)  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZZ0-CPglocSUN_jwAOrq6NrLGrMg6RVer2VFFWFQkSEcMOLDC7a-yu5NsL-fhsdRLJrV63KNiLhnaM5knfA3AGcTIOcTRIyb8XPsn8kcBC6_cAoxuH30v7DEeCWg5qrHoqSbOFglwPSk/s320/Screen+Shot+2012-04-11+at+19.18.57.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZZ0-CPglocSUN_jwAOrq6NrLGrMg6RVer2VFFWFQkSEcMOLDC7a-yu5NsL-fhsdRLJrV63KNiLhnaM5knfA3AGcTIOcTRIyb8XPsn8kcBC6_cAoxuH30v7DEeCWg5qrHoqSbOFglwPSk/s1600/Screen+Shot+2012-04-11+at+19.18.57.png)

 Going back to our image, we now have several port forwarding rules.  We add another for apache svn which pushes calls to port 9999 through to the guest.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjj-pTpnPdf2yh2fV3-MdbFhnAt7tU35kPAoFa-Da1rGr0UkQAisqmCIHHj2i95do4mPUIPKgkhh6O5H_tAvUjW4VsRdzpBIo2jSlYE8SMjg5jCgJxSwz1uagKHeWV_KgORg-rOWjV_cJ4/s320/Screen+Shot+2012-04-11+at+19.19.44.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjj-pTpnPdf2yh2fV3-MdbFhnAt7tU35kPAoFa-Da1rGr0UkQAisqmCIHHj2i95do4mPUIPKgkhh6O5H_tAvUjW4VsRdzpBIo2jSlYE8SMjg5jCgJxSwz1uagKHeWV_KgORg-rOWjV_cJ4/s1600/Screen+Shot+2012-04-11+at+19.19.44.png)

 And now we can use our host to see the new repo.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiwnu85Ju-X9nWfv_BNBHjwHb-7jgsovmYmWiC8Bm628zFavK4ZgGw5nDNLqFgjdD1pIm3kpe5-MqBboQG-iWlewuBqT6EUYhHoGriLahJlLQeq2IGy-ipg1Hrv91Zts8BaG-3C47Bgcmg/s320/Screen+Shot+2012-04-11+at+19.20.35.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiwnu85Ju-X9nWfv_BNBHjwHb-7jgsovmYmWiC8Bm628zFavK4ZgGw5nDNLqFgjdD1pIm3kpe5-MqBboQG-iWlewuBqT6EUYhHoGriLahJlLQeq2IGy-ipg1Hrv91Zts8BaG-3C47Bgcmg/s1600/Screen+Shot+2012-04-11+at+19.20.35.png)

  
  
  
After all this, we can add a user to svn so we can use it.  Primarily, me :)  
  

```
[sudo] password for oracle: 
[oracle@localhost conf]$ htpasswd -c /home/oracle/svn/repo1/
conf/       db/         format      hooks/      locks/      README.txt
[oracle@localhost conf]$ htpasswd -c /home/oracle/svn/repo1/conf/
authz          passwd         svnserve.conf  
[oracle@localhost conf]$ sudo htpasswd -c /home/oracle/svn/repo1/conf/passwd bamcgill
New password: 
Re-type new password: 
Adding password for user bamcgill
[oracle@localhost conf]$
```

  
Now we have users we can use svn. However, we need to let apache know that we want to use it.  Rememeber the  tags we filled out earlier.  Change the location tags to have the following now.  
  

```
<Location /repos>
  DAV svn
  SVNParentPath /home/oracle/svn
  AuthType Basic
  AuthName "Subversion Repository"
  AuthUserFile /home/oracle/svn/repo1/conf/passwd
  Require valid-user
</Location>
```

  
Now, we restart the httpd daemon again  

```
cd /etc/init.d
sudo ./httpd stop
sudo ./httpd start
```

  
And now we have authentication, albeit basic, but there are other blows to allow ldap and ypmaster access.   

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUKCsVzhaO-aAc7jT7vZr-_YgmkAzm8FRMpB0L0dM1AmBa_qBYQL08rT5wwZsPPXFHOoTBqsDVPVYQJKHgz95f8jaEje2zcdsxdVwKHqXiYD8fj9xqpHv_OPlaN4fVeCcAiLf7jX6XSpw/s320/Screen+Shot+2012-04-11+at+21.21.05.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUKCsVzhaO-aAc7jT7vZr-_YgmkAzm8FRMpB0L0dM1AmBa_qBYQL08rT5wwZsPPXFHOoTBqsDVPVYQJKHgz95f8jaEje2zcdsxdVwKHqXiYD8fj9xqpHv_OPlaN4fVeCcAiLf7jX6XSpw/s1600/Screen+Shot+2012-04-11+at+21.21.05.png)

  
  
Need to check in something from the directory, which we will look at in another post.    Today, we set up subversion on the Oracle Developer Day Virtual Machine.  In later posts, we'll use this to check in some code and use it with Hudson to automate some integration tasks.
