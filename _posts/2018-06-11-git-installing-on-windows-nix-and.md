---
title: "Git installing on windows, 'Nix and applications"
date: 2018-06-11 16:02:00 +0000
last_modified_at: 2018-06-11 16:02:20 +0000
tags:
  - git
  - git desktop
  - tortoisegit
  - Eclipse
  - windows
  - unix
  - osx.
---

# Getting Git installed in lots of places for a team can be a irksome.  Part of your team is running windows, maybe with Cygwin, others with various flavours on unix and osx.  Layered on top of that are the applications that we use with git services embedded in them.  This should serve as a sample page to show where we can get access to the clients and how we set them up for ssh which is our default.

# Installing git

# Overview of install at <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>.  Theres lots of different versions, but boiled up to basics are these below.

## Unix

# - sudo yum install git-all - sudo dnf install git-all (RH) - sudo apt install git-all (debian)

## windows

# - download and install <https://gitforwindows.org/>

## mac

# 1. brew install git 2. or download and install from <http://git-scm.com/download/mac>

# Connections to GitHub

We are specifically only looking at SSH connections so, heres some ways to get your keys sorted

# - generate an ssh key - add the public key to Orahub - Clone your repository

## SSH Key Generation

### Unix

# ssh-keygen -t rsa

### Windows

# Use Putty-gen . This is installed as part of the putty installation available here: <http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html>

## Add your keys to GitHub or your Enterprise Git Repo

In order to do this, its pretty specific.  You need to go to the your user settings page and click on ssh keys,  There, you can paste in your public key.  This will then let you clone your repositories with SSH as below.

## Clone Repository to local Repository

### unix terminal / cygwin

# git clone git@orahub.oraclecorp.com/restofyourrepo.git destination

### tortoisegit

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCrNAqxJ5rxsJ3VvepkahxjBZvXI9w0qM0SZzrTg-Iy0L6DqrW3WUq6a2mV9K7I20-nHdykosKv5rV9cXb6q28FvtnXZGfkG5X5pD44ropS3iXHYKGVc3QVQ5P32tFgnF8k-Mi0XDNutQ/s320/Capture3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCrNAqxJ5rxsJ3VvepkahxjBZvXI9w0qM0SZzrTg-Iy0L6DqrW3WUq6a2mV9K7I20-nHdykosKv5rV9cXb6q28FvtnXZGfkG5X5pD44ropS3iXHYKGVc3QVQ5P32tFgnF8k-Mi0XDNutQ/s1600/Capture3.png)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg7p-zBuhIJiYx3BpOpjXnvt8pwv3_0_MbeRKNQI3zsuSG7jGQ_Ql0N1wgUqtnzZ0YT-36WjN48Rik4EPJYLlDCc9HwxqRk__JdvWaihmSGA5dTuaeYnHwRrckwV_M3PPRDG-1vVf-QDKU/s320/Capture4.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg7p-zBuhIJiYx3BpOpjXnvt8pwv3_0_MbeRKNQI3zsuSG7jGQ_Ql0N1wgUqtnzZ0YT-36WjN48Rik4EPJYLlDCc9HwxqRk__JdvWaihmSGA5dTuaeYnHwRrckwV_M3PPRDG-1vVf-QDKU/s1600/Capture4.png)

### sqldeveloper

# team → Connect to git view → files

### eclipse

# window → perspective → open perspective → git repositories click clone git repository

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjd5_lm9Uh7Php3SjJD7xFBQ-gHvM0hudQFkfRR5kDA84X3Sll9vGLADeBIoFJIBbTwYFS98gQh6jXJV8iCN2UUajtox-N9ZVXjK6QizC-VVdI8Byy7xoALYLN96PBdRmgk4-1lw9AcO14/s320/Capture9.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjd5_lm9Uh7Php3SjJD7xFBQ-gHvM0hudQFkfRR5kDA84X3Sll9vGLADeBIoFJIBbTwYFS98gQh6jXJV8iCN2UUajtox-N9ZVXjK6QizC-VVdI8Byy7xoALYLN96PBdRmgk4-1lw9AcO14/s1600/Capture9.png)

### github desktop

# Download it from <https://desktop.github.com/>
