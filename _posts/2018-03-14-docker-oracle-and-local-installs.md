---
title: "Docker Oracle and local installs"
date: 2018-03-14 21:17:00 +0000
last_modified_at: 2018-03-14 21:17:16 +0000
tags:
  - macosx
  - oracle
  - Docker
  - dbtools
---

So you want Docker and to install and Oracle Database locally.  So did I and while I have [VirtualBox](https://www.virtualbox.org/) and the [Oracle Developer Day VM](https://gist.github.com/cdivilly/8082bece0ad8f819a6b4a3630699ed46), I wanted to setup docker and the Oracle Database  
Well [Colm Divilly (@cdivilly)](https://twitter.com/cdivilly) has cleared it up for me.  His [Gist](https://gist.github.com/cdivilly/8082bece0ad8f819a6b4a3630699ed46) on on Github had me up and running. Very little work on my part here, following Colm's detailed instructions, (barring time for downloads) I had docker up on mac in about 30 mins.   
  
Take a look.....  
  

## Download Database Binaries from Oracle Technology Network

Download the linux x86-64 ZIP archive from [here](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html).

## Check out the Oracle Docker Images from Github

There's a few ways to do this using an SVN or GIT client, but I just go to the project's [home page](https://github.com/oracle/docker-images), and click the button on the right hand side labeled 'Clone or Download' and then click 'Download Zip'.

Next unzip this archive of the project that you just downloaded, for example:

```
cd ~/work/docker
unzip ~/Downloads/docker-images-master.zip
```

## Move the Database Binaries to the correct location

To build the Docker image, you'll use a script named `buildDockerImage.sh`, for this script to work the Oracle Database binaries need to be placed in the correct location, for example:

```
cd ~/work/docker/docker-images-master/OracleDatabase/
mv ~/Downloads/linuxx64_12201_database.zip ./12.2.0.1
```

This places the ZIP archive containing the Oracle Database binaries in the expected `12.2.0.1` sub-folder

## Configure the Proxy if necessary

If you're behind a proxy, you'll need to ensure the `http_proxy` and `https_proxy` environment variables are set, so the proxy configuration can be propagated to the created Docker Container. If this is not done correctly then `yum` will not be able to reach any repositories.

For example:

```
export http_proxy=http://someproxy.corpdomain.com:80
export https_proxy=http://someproxy.corpdomain.com:80
```

## Build the Docker Image

To build the Docker image use the `buildDockerImage.sh` script, it's usage is described in the [README](https://github.com/oracle/docker-images/blob/master/OracleDatabase/README.md). First let's ensure the script is executable:

```
cd ~/work/docker/docker-images-master/OracleDatabase/
chmod +x ./buildDockerImage.sh
```

Next invoke the script to build the image, to build a 12.2.0.1 enterprise edition image:

```
cd ~/work/docker/docker-images-master/OracleDatabase/
./buildDockerImage.sh -v 12.2.0.1 -e
```

Go get a coffee, this step takes a while, for me it took about 16 minutes.

## Run the Docker Image

When it comes to running the Docker Image, you have several choices to make, read the [docs](https://github.com/oracle/docker-images/tree/master/OracleDatabase#running-oracle-database-in-a-docker-container) for more detail on this. I'm only going to change a few things:

- set the name of the PDB created to `ORCL`
- Store the database data on the host machine, this enables me to blow away the docker container at any time and re-create it without losing any data. In effect I'm separating the database 'engine' (the docker container) from the database storage (the volume on the host where the database storage is persisted).
- Configure the Database to use Extended Data Types (increase max VARCHAR2 to 32767 bytes).

### Prepare the storage volume

I created a folder within my home folder:

```
cd ~/work/docker
mkdir oradata
```

Note the documentation states this folder must be owned by an operating system user named `oracle`. On my Mac OS host, I found I didn't need to create an `oracle` user or give it ownership of this folder.

### Extended Data Types

In 12.1 and later VARCHAR2 fields can be configured to hold up to 32K bytes. However this feature is off by default, so we need to do some scripting to reconfigure the database to use extended data types. We want these scripts to run after the database is first setup, so we'll mount a volume as part of the `docker run` command which will cause those scripts to be executed.

The script needed is attached to this gist, so first ensure you have downloaded this script into a folder. The easiest way to do this is to click the 'Download ZIP' button at the top right of this page and then unzip the downloaded archive into a folder, for example:

```
cd ~/work/docker
mkdir db_setup_scripts
cd db_setup_scripts
unzip -j ~/Downloads/8082bece*.zip
```

- We use the `-j` option to tell unzip not to bother recreating the directory structure of the archive

We want to make sure any shell scripts are executable in the docker container, and remove unecessary files:

```
cd ~/work/docker/db_setup_scripts
chmod +x *.sh
rm *.md
```

### Run the container

Now we are all prepared, we can tell Docker to run the image, we'll give the container a name as well:

```
docker run --name oracle -p 1521:1521 -e ORACLE_PDB=ORCL \
           -v ~/work/docker/oradata:/opt/oracle/oradata \
           -v ~/work/docker/db_setup_scripts:/opt/oracle/scripts/setup \
           oracle/database:12.2.0.1-ee
```

- The `-name` argument names the container
- The `-e` arguments passed an environment variable that renames the created PDB to `ORCL` (the default is `ORCLPDB1`)
- The first `-v` argument mounts the folder to store the database data
- The second `-v` argument mounts the folder containing the scripts to convert the database to use extended data types

Time for another coffee, creating the initial database takes time. After a while the database will have been created, and the script to enable extended data types will have been executed

## Managing the Container

Once the initial setup of the database has completed, I like to stop the container and then start it again to leave it running in the background. To do this, in another terminal do the following:

```
docker stop oracle
docker start oracle
```

or simply:

```
docker restart oracle
```

### Deleting the Container

If you ever need to get rid of the container, then the following will remove the container, you can recreate it again using docker run:

```
docker stop oracle
docker rm oracle
```

## Connecting to the Database

You can use the `sqlplus` as described in the [docker images documentation](https://github.com/oracle/docker-images/tree/master/OracleDatabase#running-oracle-database-in-a-docker-container) but it's a bit hard to use because it can only read from the filesystem within the container. Much better to use it's more modern relative, [SQLcl](http://www.oracle.com/technetwork/developer-tools/sqlcl/overview/index.html), which will run anywhere you can run Java, and doesn't require an Oracle Client install, so it's super easy to get working, and especially handy for Mac users.

Since we have port forwarded the container's 1521 port to our host's 1521 port, we can use `sqlcl` to connect to the database as follows:

### Connect to the CDB

To Connect to the CDB, just do the following:

```
sql system

SQLcl: Release 4.2.0.16.043.0306 RC on Fri Sep 08 18:10:52 2017

Copyright (c) 1982, 2017, Oracle.  All rights reserved.

Password? (**********?) ******
Connected to:
Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production

SQL>
```

### Connect to the PDB

To connect to the PDB, just do the following:

```
sql system@//localhost:1521/orcl

SQLcl: Release 4.2.0.16.043.0306 RC on Fri Sep 08 18:12:29 2017

Copyright (c) 1982, 2017, Oracle.  All rights reserved.

Password? (**********?) ******
Connected to:
Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production

SQL>
```
