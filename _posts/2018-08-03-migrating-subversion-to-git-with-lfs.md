---
title: "Migrating Subversion to Git with LFS"
date: 2018-08-03 18:36:00 +0000
last_modified_at: 2019-10-11 15:21:23 +0000
tags:
  - bfg
  - git
  - subversion
  - Migration
  - lfs
  - gitlab
  - svn
---

When a project has been on the go for a while theres going to be all sorts of stuff in there from jars to zips and everything in between.  We went though this a while ago and wanting to keep all the history, we needed a way to prune the history of all the big files and weird things we were not going to move to git.   
  
Now we knew we had some large files, namely binary files like jars which were build dependencies before we moved to artifactory for a lot of it.  So, before we start we need to make sure that git is installed, and git-lfs.  Git-lfs should be on the path so git can find it and you'll need to make sure git svn can run.  You'll need perl and  to run cpan (Comprehensive Perl Archive Network) to install the SVN::Core modules.  
  

## Initialisation

As a test to start, make sure git and git lfs are on the path and that git svn runs.  
  

bamcgill@bamcgill-mac[~]

- $ git --version

git version 2.15.2 (Apple Git-101.1)

bamcgill@bamcgill-mac[~]

- $ git lfs version

git-lfs/2.3.4 (GitHub; darwin amd64; go 1.9.1)

bamcgill@bamcgill-mac[~]

- $ git svn

git-svn - bidirectional operations between a single Subversion tree and git

usage: git svn  [options] [arguments]

## Clone Empty GIT Repository

Before the migration, we should create an empty repository for importing the subversion repository into.  Then we can clone it to start the migration  
  

```
git clone git@gitlab.yourcompany.com:group-name/gitrepo.git
```

```

```

## Clone the subversion repository into the empty git repository

Before we do the clone, we need to build a file of the authors on the svn

  

```
svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > authors.txt
```

  
Now we need to edit that file which has a format like this  

bamcgill = bamcgill

to a format like this

bamcgill = Barry McGillin

  

This file is then used to map the users in subversion to the new decorated users in git.

```
git svn clone https://server.company.com/svn/project/trunk gitrepo --authors-file=authors.txt > loglog 2>&1
```

```

```

We push the output into a log file because it takes ages and you can scroll back and see where the actual clone is.  This pulls the entire history from revision 1 to HEAD and drops it into the git repository  
  

## Clean up the GIT Repository Metadata

Now, we use a really handy utility: BFG: Removes large or troublesome blobs like git-filter-branch does. For this exercise we run the utility twice. Once to strip blobs larger than 1M
  
  

```
java -jar bfg-1.13.0.jar --strip-blobs-bigger-than 1M git-repo
```

```

```

```
Now fix the changes into the repository.
```

```

```

```
cd git-repo && git reflog expire --expire=now --all && git gc --prune=now --aggressive && cd -
```

```

```

Now for the second run of the BFG, we want to convert a bunch of things like binary files to Large File Storage
  
  

```
java -jar bfg-1.13.0.jar --convert-to-git-lfs "*.{rar,dll,zip,war,gz,jar,tar,opar,dmp,serial,exe,mde,gif,msg,oxd_db,dylib,so}" --no-blob-protection git-repo
```

```

```

```
And fix that into the repository too.
```

```

```

```
cd sql-developer && git reflog expire --expire=now --all && git gc --prune=now --aggressive && cd -
```

  

## Install and Configure GIT LFS

Create an file called .lfsconfig which has your preconfigured LFS server

```
$cp lfsconfig git/.lfsconfig 
$cat .lfsconfig
[lfs]
 url = https://artifactory.yourcorp.com/api/lfs/git-lfs
```

```

```

Now, you need to install lfs into the repository.  
  

```
cd git-repo && git lfs install
```

  
and then track all the binary and large files you want  
  

```
git lfs track *.{rar,dll,zip,war,gz,jar,tar,opar,dmp,serial,exe,mde,gif,msg,oxd_db,dylib,so}
```

  

## Commit and Push

Next we need to add the files we just edited AND the base directory of the git repository as all the binary files will be swapped out to LFS on push  
  

```
git add .lfsconfig .gitattributes && git add .
```

  

```
git commit -m "initial commit to git" && git push origin master
```

  
Depending on the security setting of your artifactory repository you may be prompted for a username and password for pushing the binary files to LFS and then the references and files will be pushed to your remote git repository  
  

## Summary

It took us a couple of goes to get this right so we put it in a file to rerun when it died (it will til you get all the large file extensions listed)  
Heres the contents of that script you can grab and use for your migration.  
Have fun.  
  

git clone git@gitlab.yourcompany.com:group-dev/git-repo.git && \

git svn clone https://svn.yourcompany.com/svn/project/trunk git-repo --authors-file=authors.txt > loglog 2>&1 && \

java -jar bfg-1.13.0.jar --strip-blobs-bigger-than 1M git-repo && \

cd git-repo && git reflog expire --expire=now --all && git gc --prune=now --aggressive && cd - && \

java -jar bfg-1.13.0.jar --convert-to-git-lfs "\*.{rar,dll,zip,war,gz,jar,tar,opar,dmp,serial,exe,mde,gif,msg,oxd\_db,dylib,so}" --no-blob-protection git-repo && \

cd git-repo && git reflog expire --expire=now --all && git gc --prune=now --aggressive && cd - && \

cp lfsconfig git-repo/.lfsconfig && \

cd git-repo && \

git lfs install && \

git lfs track \*.{rar,dll,zip,war,gz,jar,tar,opar,dmp,serial,exe,mde,gif,msg,oxd\_db,dylib,so} && \

git add .lfsconfig .gitattributes && \

git add . && \

git commit -m "initial commit to git" && \

  

git push origin master
