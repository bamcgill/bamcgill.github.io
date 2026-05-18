---
title: "Add a new hard drive to your Oracle Developer Days VM"
date: 2012-05-09 11:59:00 +0000
last_modified_at: 2012-05-09 11:59:11 +0000
tags:
  - oracle
  - virtualbox
  - Oracle Developer Day VM
  - SQL Developer
  - linux
---

For those of you who end up using the [Oracle Developers Day VM](http://www.oracle.com/technetwork/community/developer-vm/index.html) for more that just demo's but playing with other things too, will find that at some point, you'll need more space. (Like I did)   Today's post is about just that.  We're going to add a new VMDK drive to our virtual machine and configure it so its available to you in the machine.  
  
  
First thing we want to do is to have a list of the devices in your linux box.  This will save you searching for it once you add it later.  
  
  

```
[oracle@localhost ~]$ cd /dev
[oracle@localhost dev]$ ls -al hd*
brw-r----- 1 root disk  3,  0 May  4 05:50 hda
brw-r----- 1 root disk  3,  1 May  4 05:51 hda1
brw-r----- 1 root disk  3,  2 May  4 05:50 hda2
brw-r----- 1 root disk  3, 64 May  4 05:50 hdb
brw-r----- 1 root disk  3, 65 May  4 05:51 hdb1
[oracle@localhost dev]$
```

  

Now we can power down the machine and add the drive.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg8ViQnaVwirWzdi84SjYeYR6uWSCHfGqKBnczAmIEOAjWvLeuNxS6jBIVSM158pAFXdZI5IV8gFStJI8_zF-L5_Iaxu8w1c2qnsg0EJFcZKYKupASOM30yE-iUg64__ZMaGUfY4zd53G4/s1600/Screen+Shot+2012-05-04+at+13.22.52.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg8ViQnaVwirWzdi84SjYeYR6uWSCHfGqKBnczAmIEOAjWvLeuNxS6jBIVSM158pAFXdZI5IV8gFStJI8_zF-L5_Iaxu8w1c2qnsg0EJFcZKYKupASOM30yE-iUg64__ZMaGUfY4zd53G4/s1600/Screen+Shot+2012-05-04+at+13.22.52.png)

  
  
You need to make sure your VM is powered down so we can make changes to the server.  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi7zcUX3D8l-uSNrb577wj8X1DgD9RECjRnDw-hffKk3lMwt3wBV9NDq-k1oh8dM25RSI0_LPwYX_ribux6pfb-TgURwI1X5B-_AF4Q5GzNBmElvU-3Ii0nt_taRAVzDAvC6le3Fyg1jgo/s320/Screen+Shot+2012-05-04+at+13.23.09.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi7zcUX3D8l-uSNrb577wj8X1DgD9RECjRnDw-hffKk3lMwt3wBV9NDq-k1oh8dM25RSI0_LPwYX_ribux6pfb-TgURwI1X5B-_AF4Q5GzNBmElvU-3Ii0nt_taRAVzDAvC6le3Fyg1jgo/s1600/Screen+Shot+2012-05-04+at+13.23.09.png)

  
  
Checking the storage frame of this VM, we can see that there is only two drives connected.  Double clicking on the storage frame pops up the storage window where we can add the drive.  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLp54fgAgk7MZtSdUQc9xZ07j01VXQq4UvN_OENRvSWdL7v645D5kO9pDE7VVTPuRP6iu-i5Pwty3l1xQXhH-uMZR850mAIxR7TbdP66iY6ARMYdcpMGji7v1vfv24vRMdUpl7sIO_r_Q/s320/Screen+Shot+2012-05-04+at+13.23.30.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLp54fgAgk7MZtSdUQc9xZ07j01VXQq4UvN_OENRvSWdL7v645D5kO9pDE7VVTPuRP6iu-i5Pwty3l1xQXhH-uMZR850mAIxR7TbdP66iY6ARMYdcpMGji7v1vfv24vRMdUpl7sIO_r_Q/s1600/Screen+Shot+2012-05-04+at+13.23.30.png)

  
Clicking on add drive, asks us if we want to add an already built drive or add a new one.  We want to add a new one.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgcUof30RjPAiHgnGVJaCNVGa5A7Dh2NBVNwfoU8WFWnRm1egRvf_9HCKJSr0F8S_cCdBXY5bkfgzhPleEjCSQIUuNcaZZJM55FIUb_8hP2m3k_rQNZejazK5lzW9IvjoVHWH-HstexV98/s320/Screen+Shot+2012-05-04+at+13.23.50.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgcUof30RjPAiHgnGVJaCNVGa5A7Dh2NBVNwfoU8WFWnRm1egRvf_9HCKJSr0F8S_cCdBXY5bkfgzhPleEjCSQIUuNcaZZJM55FIUb_8hP2m3k_rQNZejazK5lzW9IvjoVHWH-HstexV98/s1600/Screen+Shot+2012-05-04+at+13.23.50.png)

  
We then choose a VMDK to use.  There are other types, but we're using this one for now.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiqMs7pV6TQkZDJBfVxVx2lZRuJdQXvm6d64lbUf8zvhwzOMet0lJoS_nKBR4Oqi389ol5UBKvjvGn9kOmnuxiXX2HAAd5k-B3hGb2ctx7NlqSnfyXKmuahawxtusQj5bT5-QyDwesLEMU/s1600/Screen+Shot+2012-05-04+at+13.24.06.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiqMs7pV6TQkZDJBfVxVx2lZRuJdQXvm6d64lbUf8zvhwzOMet0lJoS_nKBR4Oqi389ol5UBKvjvGn9kOmnuxiXX2HAAd5k-B3hGb2ctx7NlqSnfyXKmuahawxtusQj5bT5-QyDwesLEMU/s1600/Screen+Shot+2012-05-04+at+13.24.06.png)

  
On the next page of the wizard, we choose dynamically allocated. which will size the disk to just the be the size of the data that is in it.  So if there is no data on the drive, this file will be tiny.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigyeZxJDbtaoG0sxnm5N6plvkdyHdrcT2u2WvEivUjQC8HLMdmcvCQZkghEUCpQQZqpMnTcIYQeHqPnYDHDmfTfhJlOdSGXCA2maeL4duOP9BHez8NeKhH0G3_nnFLmsu6TD8PiX0YgbA/s1600/Screen+Shot+2012-05-04+at+13.24.14.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigyeZxJDbtaoG0sxnm5N6plvkdyHdrcT2u2WvEivUjQC8HLMdmcvCQZkghEUCpQQZqpMnTcIYQeHqPnYDHDmfTfhJlOdSGXCA2maeL4duOP9BHez8NeKhH0G3_nnFLmsu6TD8PiX0YgbA/s1600/Screen+Shot+2012-05-04+at+13.24.14.png)

  
Next we give it a name and size.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUfpTpJ6kuTmZ0RyEJz5uORbPXq-rOCy7ocVYG_Mr-wjNsGc-gy51iGitHYXsmfgi2eerjsvXnjsqrzOEwXTKXJOW71cCnb4KcSuE8Qs3TXhGdDsIh4NBgf2YVM5rkaOEX8QyaCtYih_A/s320/Screen+Shot+2012-05-04+at+13.25.05.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUfpTpJ6kuTmZ0RyEJz5uORbPXq-rOCy7ocVYG_Mr-wjNsGc-gy51iGitHYXsmfgi2eerjsvXnjsqrzOEwXTKXJOW71cCnb4KcSuE8Qs3TXhGdDsIh4NBgf2YVM5rkaOEX8QyaCtYih_A/s1600/Screen+Shot+2012-05-04+at+13.25.05.png)

  
Clicking ok to finish the wizard show the new drive added.  One las thing we do is to change the type of the hard drive to be a secondary slave.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgw1LdKXO_ylh1HQ2zeuS_vx4BWJN6b7ZDsxTkD9ZexhpBSgJMvva8OZNgiPyvkqW7sQ8fjpp17Erg-TV1ChvtqnOJWjyoYaRGLAeOFhUsD6HSJRnRyw5hMvQQEIX1LUevZlp_KbOwdsRY/s1600/Screen+Shot+2012-05-04+at+13.25.17.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgw1LdKXO_ylh1HQ2zeuS_vx4BWJN6b7ZDsxTkD9ZexhpBSgJMvva8OZNgiPyvkqW7sQ8fjpp17Erg-TV1ChvtqnOJWjyoYaRGLAeOFhUsD6HSJRnRyw5hMvQQEIX1LUevZlp_KbOwdsRY/s1600/Screen+Shot+2012-05-04+at+13.25.17.png)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZ1AIcbT38WxRPh6xHYTUxmaFeBf8FsxtaEfeXLY-qCOq-jireMps5wwmIi7DcOjjYvNigY2qLs0Bs194hPKCEiUo9_cSekOdaIrCXiv1GtBd8Oy7UErtd7P1urd9dSlKW8IXp1RwTpNM/s1600/Screen+Shot+2012-05-04+at+13.25.42.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZ1AIcbT38WxRPh6xHYTUxmaFeBf8FsxtaEfeXLY-qCOq-jireMps5wwmIi7DcOjjYvNigY2qLs0Bs194hPKCEiUo9_cSekOdaIrCXiv1GtBd8Oy7UErtd7P1urd9dSlKW8IXp1RwTpNM/s1600/Screen+Shot+2012-05-04+at+13.25.42.png)

  
And there we have it, one file added.  This is useless to us though until we go in and format configure it in linux, then bring it online so its of use to us.  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiQBWB6Lshm5ZzcI_Uwi3Jslbv56allHVSxLWxcqc47NYbvo8pAjvSI6tKHS01rstq-TZ1Tlah4VVZzs9XV-m7zw6BTaSbyUsygDB_nOXxB0kXhiBL_2m-ZdlDwfT9W7nlp5Qz23oXfmag/s1600/Screen+Shot+2012-05-04+at+13.25.50.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiQBWB6Lshm5ZzcI_Uwi3Jslbv56allHVSxLWxcqc47NYbvo8pAjvSI6tKHS01rstq-TZ1Tlah4VVZzs9XV-m7zw6BTaSbyUsygDB_nOXxB0kXhiBL_2m-ZdlDwfT9W7nlp5Qz23oXfmag/s1600/Screen+Shot+2012-05-04+at+13.25.50.png)

  
  
Ok, Now we have a drive attached to our virtual machine.  All that remains is for us to configure it in in the machine so it is formatted and mounted.  
  
  
Firing up the VM as normal, we want to SU as root for the next phase.  The first thing we need to do is to format the disk.  
  

```
[oracle@localhost ~]$ cd /dev
[oracle@localhost dev]$ ls -al hd*
brw-r----- 1 root disk  3,  0 May  4 05:50 hda
brw-r----- 1 root disk  3,  1 May  4 05:51 hda1
brw-r----- 1 root disk  3,  2 May  4 05:50 hda2
brw-r----- 1 root disk  3, 64 May  4 05:50 hdb
brw-r----- 1 root disk  3, 65 May  4 05:51 hdb1
brw-r----- 1 root disk  3, 65 May  4 05:53 hdd
[oracle@localhost dev]$
```

  
Now looking at the top device listing versus this one we can see that the new device that has been add is /dev/hdd  
  
  
This disk that we've added is blank and raw so the first thing we need to do is to set up partitions and then format the disk.  
  

```
[oracle@localhost dev]$ sudo fdisk /dev/sdd

Command (m for help): m
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)

Command (m for help):
```

  
Choose 'n' to create a new partition and then choose 'e' and then pick the defaults through that option.  
  

```
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
```

  
Finally, when this comes back, choose the 'w' to write the partition table back to disk.  
  

```
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
[oracle@localhost dev]$
```

  
Now we can build the file system on the disk we have partitioned with mkfs.  
  

```
[oracle@localhost dev]$  sudo mkfs -t ext3 /dev/sdd
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
6111232 inodes, 12211400 blocks
610570 blocks (5.00%) reserved for the super user
First data block=0
373 block groups
32768 blocks per group, 32768 fragments per group
16384 inodes per group
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
        4096000, 7962624, 11239424

Writing inode tables: done                            
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done

[oracle@localhost dev]$
```

  
Now you have a drive, but its not mounted anywhere so you still cant see it.    You will now need to create a mount point for your drive in the root file system.
  
  

```
[oracle@localhost ~]$ sudo mkdir -p /newdrive
[sudo] password for oracle: 
[oracle@localhost ~]$
```

  
 And lastly you can issue the mount command to mount the drive to that mount point.  
  

```
[oracle@localhost ~]$ sudo mount -t ext3 /dev/hdd /newdrive
[oracle@localhost ~]$
```

  
Now you can list your drive with 'ls -al /newdrive' and it is listed and usable.  However, the next time, the machine is rebooted, you will not have this drive mounted.  We need to add a line to the file /etc/fstab to allow it to be mounted automatically.  
  

```
LABEL=/                 /                       ext3    defaults        1 1
LABEL=/home             /home                   ext3    defaults        1 2
tmpfs                   /dev/shm                tmpfs   defaults        0 0
devpts                  /dev/pts                devpts  gid=5,mode=620  0 0
sysfs                   /sys                    sysfs   defaults        0 0
proc                    /proc                   proc    defaults        0 0
LABEL=SWAP-hda2         swap                    swap    defaults        0 0
http://localhost:80     /home/oracle/dav        davfs   noauto,users    0 0
/dev/hdd                /newdrive               ext3    defaults        1 2
```

  
Adding the line above to this file will allow the drive to be mounted each time the machine reboots.    
  
  
Now you have a drive which you can use for data or install other Oracle software on, like Oracle Golden Gate  to help synchronise data between databases.  Find out more about the [Oracle developer day VM](http://www.oracle.com/technetwork/database/enterprise-edition/databaseappdev-vm-161299.html) on [OTN](http://otn.oracle.com/)
