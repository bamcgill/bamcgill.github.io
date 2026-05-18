---
title: "Using the Oracle Developer Days VirtualBox Image"
date: 2011-12-07 09:07:00 +0000
last_modified_at: 2011-12-07 11:11:37 +0000
tags:
  - laptop
  - virtualbox
  - network adapters
  - configuration
  - SQLDEVELOPER
---

As many of you know @krisrice put together a great VM for the Oracle Developer Days and while the content is great for education, I find us using it more and more a default scratch database on laptops.  As usual, being 'Networkly challenged', it took me some time to figure out which network adapters did what and why.  This is as much a note for me as it is to share with you :).  
  
First of all, you need to install VirtualBox, which is found [here](http://www.oracle.com/technetwork/server-storage/virtualbox/overview/index.html).  Then download one of the prebuilt VirtualBox images for the Developer Days.  You can choose your one [here](http://www.oracle.com/technetwork/community/developer-vm/index.html).  Download the ova file and then import your VM into VirtualBox.   
  
To import, choose File> Import Appliance in VirtualBox and click choose to select the directory where you want the VM to live, then select your ova file.  In this example, I'm using @krisrice's Oracle DeveloperDays VM. Once you click finish, and agree to the licenses, you'll see the 'Oracle Developer Days' VM in VirtualBox with a powered off state.   

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi6al3KnV6D7VspvxWkklxygViuSv02OGlBQESOMuvNIy2g8z5vvC1yaobbo0hy4dIJhRery7xyTz9uI90P6KFFpfNUdLVnJ9sUMjF7-KbriIYzYNaLaQ28xtyzJ1rGaHBr07ebQhfdFZA/s320/Untitled.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi6al3KnV6D7VspvxWkklxygViuSv02OGlBQESOMuvNIy2g8z5vvC1yaobbo0hy4dIJhRery7xyTz9uI90P6KFFpfNUdLVnJ9sUMjF7-KbriIYzYNaLaQ28xtyzJ1rGaHBr07ebQhfdFZA/s1600/Untitled.png)

  
Great.  We're ready to fire up the box and play inside it.  All passwords for this are 'oracle', so you cant go wrong. In this, the database is all setup automatically, as is this list of stuff.  
  

- Oracle Linux 5
- Oracle Database 11g Release 2 Enterprise Edition
- Oracle TimesTen In-Memory Database Cache
- Oracle XML DB
- Oracle SQL Developer
- Oracle SQL Developer Data Modeler
- Oracle Application Express
- Oracle JDeveloper
- Hands-On-Labs (accessed via the Toolbar Menu in Firefox)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEivXeQFRaRB0pRYoZerhQdU28N15UBQJ03-zmcEuFzRC6_NlIedPx-53G1v1M2l_qyaQhhRYzz00wWzAYq9Cb_fdrdSxKKQ8k3AMnWWBq1pcDtJXuf4-h2UyJcjWClJ7rQ9xdXpZGl0MoM/s320/linux.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEivXeQFRaRB0pRYoZerhQdU28N15UBQJ03-zmcEuFzRC6_NlIedPx-53G1v1M2l_qyaQhhRYzz00wWzAYq9Cb_fdrdSxKKQ8k3AMnWWBq1pcDtJXuf4-h2UyJcjWClJ7rQ9xdXpZGl0MoM/s1600/linux.png)

  
  
So now, login to the vm with oracle/oracle and a terminal window will show you whats available and the network profiles you setup in the VM settings.  The network settings I setup for this is here  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYTFZooZ2dcARMXNIB1SqSDEqroMWSEyV_nMJr6-SfaC9CnR_FsmNruW3Do32RqVQd7Y2PckgsMfduN-L9nYq3N1Zp6Uaov4mB9Bz54ezwmhx6An9efQn5cTu1B2rnwZzGCGpdcssqHKM/s320/networkvb.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYTFZooZ2dcARMXNIB1SqSDEqroMWSEyV_nMJr6-SfaC9CnR_FsmNruW3Do32RqVQd7Y2PckgsMfduN-L9nYq3N1Zp6Uaov4mB9Bz54ezwmhx6An9efQn5cTu1B2rnwZzGCGpdcssqHKM/s1600/networkvb.png)

These two adapters do separate things.  The bridged adapter will assign an IP address from the wireless NIC.  This is setup by default when you install the VM and allows you to get access to the internet from the VM.  The NAT adapter will allow you to access the VM from the host machine when you have no physical NIC or internet available.  This happened me yesterday when presenting some SQLDeveloper functionality.  By enabling the NAT adapter and setting up a few port forwarding rules, we can ssh into the VM and connect SQL Developer to the normal LISTENER port.  
The NAT adapter looks like this.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiMrW8VK0p3EA9XQBxoBm9rn8KbDupL0shEBuvXaT9n6XdCQgDr_hfOzuZLscM3NdWZOSJA4D1n6szyBfheBHrzzOKmqnIVnIY7dswjuwL4-v2UxrMcYIdDo_VSpXvRreZZCfNGJ417clE/s320/NATadaptersetting.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiMrW8VK0p3EA9XQBxoBm9rn8KbDupL0shEBuvXaT9n6XdCQgDr_hfOzuZLscM3NdWZOSJA4D1n6szyBfheBHrzzOKmqnIVnIY7dswjuwL4-v2UxrMcYIdDo_VSpXvRreZZCfNGJ417clE/s1600/NATadaptersetting.png)

  
and setting up two port forwarding rules, gives us this  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQEkXR_AdXIxS1jfO7vpwQz1Z5-0Is6hZA2EdWcJ06Ov9fwQ00_fxQRUfie81mDpHYTBkOuxU4JzeNmFNXcWRmjdq_iH4ADO6AYQExGacUzLENQzDuVva_A_hDsI8W5yDksz0yAG7gKTE/s320/portforwarding.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQEkXR_AdXIxS1jfO7vpwQz1Z5-0Is6hZA2EdWcJ06Ov9fwQ00_fxQRUfie81mDpHYTBkOuxU4JzeNmFNXcWRmjdq_iH4ADO6AYQExGacUzLENQzDuVva_A_hDsI8W5yDksz0yAG7gKTE/s1600/portforwarding.png)

When you login to the VM, you'll see this on the terminal window.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjKBCf3sZlun3YufDzNt8SLddj4_uvl4WIiJcPm8MLuaIpIgMoo1-Amy0XvqQL4nfTA13fe9Ym5HKPhn-FSRlA4VPElf3cwib9Ut95L4aWoBFI4z4goKWEOhyNObcG_-UsoJKQH9jmH46U/s320/terminaldetails.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjKBCf3sZlun3YufDzNt8SLddj4_uvl4WIiJcPm8MLuaIpIgMoo1-Amy0XvqQL4nfTA13fe9Ym5HKPhn-FSRlA4VPElf3cwib9Ut95L4aWoBFI4z4goKWEOhyNObcG_-UsoJKQH9jmH46U/s1600/terminaldetails.png)

This setup will allow you to spark up firefox in the VM and connect to the internet using the local network ip 192.168.1.42.  Now, if we switch off the Airport and disable the bridging adapter, we should still be able to connect to the VM from outside.  Restarting the VM, gives us this terminal window on login to the oracle account  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhC3hDulGQOsWeNiCCcqbGLPZdoAeysADGVCcMcRSYCyupbVjfSoSUnTicRjpwRea2oaAW4XIrCBgc7PspwAIDGDcA0fv79pvqyoZqIBUcKjhL7iTehRre_ZHiImEvC3HsccK5sGidpQ2Q/s320/terminal2.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhC3hDulGQOsWeNiCCcqbGLPZdoAeysADGVCcMcRSYCyupbVjfSoSUnTicRjpwRea2oaAW4XIrCBgc7PspwAIDGDcA0fv79pvqyoZqIBUcKjhL7iTehRre_ZHiImEvC3HsccK5sGidpQ2Q/s1600/terminal2.png)

Now, we have no external IP, but we have our port forwarding rules set up to get access to the VM from outside.  Now, we have two rules, one which maps anything on port 2222 to port 22 on the guest.  this means we can ssh into the VM on port 2222 on the host. So, connecting with this  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEis_u4WTsEJrtpX6bvN7jW223NBcr_DgPBXMbFEBB-sNFIQzuzLk34CfkqM8Jc8qN9S-sTCaEFnh8wnEjFvmS56hFxCYAroFHycxYWhGmKQJO2clQKQaUtkyd5jnQ32rqmvxbhhkOq_KOI/s320/externTerm.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEis_u4WTsEJrtpX6bvN7jW223NBcr_DgPBXMbFEBB-sNFIQzuzLk34CfkqM8Jc8qN9S-sTCaEFnh8wnEjFvmS56hFxCYAroFHycxYWhGmKQJO2clQKQaUtkyd5jnQ32rqmvxbhhkOq_KOI/s1600/externTerm.png)

and we get the login terminal from the VM  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUcWp2aM4TnwTgs2cc85cbYLMBaYVDLkqRSastWqZEdzG52WgPZ_ykSQL9Pc-fP-N9Mrx_AGg5bsGobj16f2tLOqL0PZwSfADooWSS0qJSCSOAb3ooUsXSYvJ4226xL65WQ1yST1nPgpA/s320/termconnected.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUcWp2aM4TnwTgs2cc85cbYLMBaYVDLkqRSastWqZEdzG52WgPZ_ykSQL9Pc-fP-N9Mrx_AGg5bsGobj16f2tLOqL0PZwSfADooWSS0qJSCSOAb3ooUsXSYvJ4226xL65WQ1yST1nPgpA/s1600/termconnected.png)

Brilliant.  Now, Lets see SQL Developer connect to the VM too.  We setup the connection like a connection to xe on localhost, except the SID is orcl on the VM.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjuJ_QlbJWC36gYWa3k9pKNdNLi8WPB2Fpd54lb2HnucZ2GbdiHYx0vbtEPpyru9orlHCma1QBv3pZvQI6kXP_qWhKMwoBKALD5FWEnXePz3GhwgT2oGMBIMkYvOkj8MKt-45dWFaJZNjc/s320/sqldevconn.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjuJ_QlbJWC36gYWa3k9pKNdNLi8WPB2Fpd54lb2HnucZ2GbdiHYx0vbtEPpyru9orlHCma1QBv3pZvQI6kXP_qWhKMwoBKALD5FWEnXePz3GhwgT2oGMBIMkYvOkj8MKt-45dWFaJZNjc/s1600/sqldevconn.png)

and we can look at the database version report which shows us what database we are connected to  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhgCyi3t2D9BA5MviUNQdjqUKsbpVrr_D8OjbjhQiWlGJZhyphenhyphenhC3ARMoVz6corFIBAVYjjFFTLruHp-EOZGIF5h0cXlpJL4h2-0XtYaapazgcaR9rnve4WN-COQPz1rNrzzgP-3CsVBn3Oc/s320/version.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhgCyi3t2D9BA5MviUNQdjqUKsbpVrr_D8OjbjhQiWlGJZhyphenhyphenhC3ARMoVz6corFIBAVYjjFFTLruHp-EOZGIF5h0cXlpJL4h2-0XtYaapazgcaR9rnve4WN-COQPz1rNrzzgP-3CsVBn3Oc/s1600/version.png)

And now, you're connected and good to go.  This is great for doing demos in a canned environment, especially when you dont have access to an internet connection when doing a demo or showing something off.
