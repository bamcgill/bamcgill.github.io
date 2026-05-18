---
title: "Configuring MySQL on EL5, Setting Passwords and Network Access"
date: 2013-08-24 15:35:00 +0000
last_modified_at: 2013-08-24 15:35:34 +0000
tags:
  - oracle
  - passwords
  - configuration
  - MySQL
  - SQL Developer
  - network
---

I find myself installing and running mysql of different versions in different places for different reasons all the time (well often enough to do it and not remember the little things that cost time when setting up)   Its with that in mind, I'm making notes for myself and you guys as well to help you along.  
  
We use MySQL a lot with [Oracle SQLDeveloper](http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html) and many use SQLDeveloper to co-exist between MySQL and Oracle.  
  
For most versions of Oracle Linux, we will install SQL Server from the Yum repository. If you dont have one set up you can configure one under /etc/yum.repos.d.  These notes for yum are a reference (blatant copy) from the [Oracle Linux Admin guide](http://docs.oracle.com/cd/E37670_01/E37355/html/ol_downloading_yum_repo.html)  

1. As `root`, change directory to `/etc/yum.repos.d`.

   ```
   # cd /etc/yum.repos.d
   ```
2. Use the `wget` utility to download the repository configuration file that is appropriate for your system.

   ```
   # wget http://public-yum.oracle.com/public-yum-release.repo
   ```

   For Oracle Linux 6, enter:

   ```
   # wget http://public-yum.oracle.com/public-yum-ol6.repo
   ```

   The `/etc/yum.repos.d` directory is updated with the repository configuration file, in this example, `public-yum-ol6.repo`.
3. You can enable or disable repositories in the file by setting the value of the `enabled` directive to 1 or 0 as required.

Now we are ready to install MySQL. If you havent used yum before play with some of the options to list packages and switch repos as you need them.  Its a great tool saving us all lots of time with dependencies.  
  

```
root@localEl5# yum install mysql-server
```

You can see if its installed by doing  

```
root@localEl5> yum list mysql-server
Loaded plugins: security
el5_latest                      | 1.4 kB     00:00  
Installed Packages
mysql-server.i386        5.0.95-5.el5_9    installed
root@localEl5>
```

You can then start it with  

```
root@localEL5> /etc/init.d/mysqld start
```

and check its running by  

```
root@localEL5> /etc/init.d/mysqld status

mysqld (pid 31298) is running...
```

In general, you can start mysql on the server without a server password in order to set one up for yourself. My one caveat here, is that all this is for development folks, some one with a security hat on will complain (bitterly).  I'm going to show you how to clear down all permissions so you can connect from any machine.

```
root@localEL5> /etc/init.d/mysqld stop
root@localEL5> /etc/init.d/mysqld status
root@localEL5> mysqld_safe --skip-grant-tables &amp;
mysql -uroot
```

Now we are logged into mysql as root with no passwords.  We can check what users are here and what permissions they have. Now, in this case, I have 
  

```
mysql> select user, host, password from user; 
 +-------+-------------+-------------------------------------------+
| user  | host         | password                                  |
+-------+--------------+-------------------------------------------+
| root  | localhost    | *2447D497B9A6A15F2776055CB2D1E9F86758182F | 
| root  | 192.168.1.201| *2447D497B9A6A15F2776055CB2D1E9F86758182F | 
| barry | localhost    | *2447D497B9A6A15F2776055CB2D1E9F86758182F | 
+-------+--------------+-------------------------------------------+
```

The first thing I want to do is to remove duplicate entries for my user  

```
mysql> delete from user where user='root' and host ='192.168.1.201';
```

now we have
  

```
+-------+--------------+-------------------------------------------+
| user  | host         | password                                  |
+-------+--------------+-------------------------------------------+
| root  | localhost    | *2447D497B9A6A15F2776055CB2D1E9F86758182F | 
| barry | localhost    | *2447D497B9A6A15F2776055CB2D1E9F86758182F | 
+-------+--------------+-------------------------------------------+
```

Now, next I want to update the hosts to any host which is '%' in mysql
  
  

```
 mysql> update user set host='%';
```

  
which now gives me
  

```
+-------+------+-------------------------------------------+
| user  | host | password                                  |
+-------+------+-------------------------------------------+
| root  | %    | *2447D497B9A6A15F2776055CB2D1E9F86758182F | 
| barry | %    | *2447D497B9A6A15F2776055CB2D1E9F86758182F | 
+-------+------+-------------------------------------------+
2 rows in set (0.00 sec)
```

Now, if you want to change your passwords, make sure you do that now.  If you are on 5.1 and over secure\_auth is set on and old passwords are off  by default. In my version 5.0, I need to set them to get new passwords and secure\_auth which is default on all mysql clients now.  This is done in /etc/my.conf followed by a restart of mysql

```
old_passwords=0
secure-auth=1

mysql> update user set password=PASSWORD('oracle') where user='root';
```

  
lastly flush privileges and exit  
  

```
mysql> flush privileges;
```

Lastly, I like my prompts to be informative so, You can also set this in your profile to setup your prompts.

```
export MYSQL_PS1="\u@\h [\d] > "
```

It'll give you a prompt like this when I log in with   
  

```
root@localEl5> mysql -uroot -poracle -Dmysql
```

giving this prompt in mysql

```
root@localEL5 [mysql] >
```

Now, you are all set to connect from SQL Developer to the this instance.  We can also install the sample databases from http://dev.mysql.com/doc/index-other.html
