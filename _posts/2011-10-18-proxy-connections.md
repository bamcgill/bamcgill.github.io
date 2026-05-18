---
title: "Proxy Connections"
date: 2011-10-18 13:06:00 +0000
last_modified_at: 2011-10-24 22:42:24 +0000
tags:
  - Connections
  - oracle
  - SQLDEVELOPER
  - proxy_user
  - worksheet
  - sqlplus
---

While looking at some issues with specific connection upgrades, I've been playing with proxy connections in SQL Developer, and while easy to do, can be interesting to get your head around. There are a number of things to do which are important. So, Lets start with a proxy user called proxy and a target user called target. (Nice and original)  

```
drop user proxy cascade;
drop user target cascade;
create user proxy identified by proxy;
create user target identified by target;
alter user target grant connect through proxy;
grant create session to proxy;
grant connect, resource to target;
connect target/target;
create table target (id number);
insert into target values (1);
connect proxy[target]/proxy;
show user
select * from target;
```

  
This set of commands run as Sys in the worksheet will create the two users. The proxy privilege is granted using  
  

```
alter user target grant connect through proxy;
```

  
The target user is granted resource role to create a table, in this case, we call it target and put some data in it. Next, we can connect to the target user, through the proxy using  
  

```
connect proxy[target]/proxy;select * from target;
```

  
This all gives us this feedback including the user which is actually connected.  
  

```
user PROXY dropped.user TARGET dropped.user PROXY created.user TARGET created.user TARGET altered.grant succeeded.grant succeeded.Connectedtable TARGET created.1 rows inserted.ConnectedUSER is TARGETID-- 1 Connection created by CONNECT script command disconnected
```

  
We can also set this up in SQL Developer using the connection dialog. Given the users have been created as above and the appropriate privileges have been granted, we can set this up in the dialog  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjm5gIozSUZZ-7OpFIYmV_g0gBCipDO43vjIjUIrXdajpv9Hmazh2ZYFjaK_ZIMAyI8gMNDEjtvy_eC2qRPoPKDo9EqxGJPsGcIV19OY6UzPqN-j9G1t9AZhb_j3VS0rhRwNesMmu5XK68/s320/proxy.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjm5gIozSUZZ-7OpFIYmV_g0gBCipDO43vjIjUIrXdajpv9Hmazh2ZYFjaK_ZIMAyI8gMNDEjtvy_eC2qRPoPKDo9EqxGJPsGcIV19OY6UzPqN-j9G1t9AZhb_j3VS0rhRwNesMmu5XK68/s1600/proxy.PNG)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHna2kEN3CgHaqPKbj7IOzRzeIMEFEMsha_ZopWcG2hr29SN2XW6_30gOoOFr-3RUP8u440MZvBgUcYYgKVwwgAp9bQ9YxjSClhOq7I_fDM2UvT-3p_7AAqvZMB832As3gYecYarKACcY/s1600/proxy_connected.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHna2kEN3CgHaqPKbj7IOzRzeIMEFEMsha_ZopWcG2hr29SN2XW6_30gOoOFr-3RUP8u440MZvBgUcYYgKVwwgAp9bQ9YxjSClhOq7I_fDM2UvT-3p_7AAqvZMB832As3gYecYarKACcY/s1600/proxy_connected.PNG)Once we make the connection, we can expand the table tree and see the target table from the user we proxied into to.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhCdYc_2e3TEHTySh9FwnvNGfBAXNcWAoxBKwHoJkB5IoMIXJtUdzc5BqhsLpntD3LJJ6e4b6Daz2gblB81-3_CYENPvfxMkupuLVC6S6O99bQNh8AdibF-zh_TGouUHcRMyEgp1DtI8So/s1600/proxy_target_data.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhCdYc_2e3TEHTySh9FwnvNGfBAXNcWAoxBKwHoJkB5IoMIXJtUdzc5BqhsLpntD3LJJ6e4b6Daz2gblB81-3_CYENPvfxMkupuLVC6S6O99bQNh8AdibF-zh_TGouUHcRMyEgp1DtI8So/s1600/proxy_target_data.PNG)  
The data is exactly the same as the data from the Worksheet script output as well.  
  
  

One thing I did forget to mention was the ability to create distinguished proxies as well. You do the same thing with the connection panels and but switch to disctinguished name. You can set up a distinguished user doing the following.

  
  

```
drop user dproxy cascade;
create user dproxy identified globally as 'CD=dproxy,OU=europe,O=oracle,L=omagh,ST=tyrone,C=ie';
alter user dproxy grant connect through barry authenticated using distinguished name;
```
