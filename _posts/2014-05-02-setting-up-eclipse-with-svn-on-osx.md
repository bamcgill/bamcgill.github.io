---
title: "Setting up Eclipse with SVN on OSX Mavericks "
date: 2014-05-02 15:49:00 +0000
last_modified_at: 2014-05-02 15:49:43 +0000
tags:
  - Eclipse
  - Mavericks
  - MACOS
  - javaHL
  - SVNKit
  - svn
  - subclipse
---

So My macbook pro died the other day and much to my wife's amusement, my dell laptop died 30 minutes later with disk errors as I hadn't used in it in forever.  She wasn't laughing long though cos I swiped her Macbook Air to get me out of a hole while the Apple store replace the magsafe card. (Don't worry, though, cos Lisa grabbed one of the kids laptops and now they are the only ones fuming. )  
  
So, here we are, no development environment to speak of on this laptop, not even Xcode tools or anything and a release to go out!  First thing out of the box was to down load eclipse, from eclipse.org, which at time of writing is still [keplar](https://www.eclipse.org/downloads/index-developer.php?release=kepler).   

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiqIuS6d_yBrrLyuFUETwzdQcbNzdks0a_tZDyZIwUyUcLJzezzuXJD37C_MciDNT0ZPPAYDJQx8m_VDKtrTM9GSdOo-vWYKlOUhiYInY_Quw0iKN_j3txgGs7F7UvPeFMiQI2ikIXerdA/s1600/Screen+Shot+2014-05-02+at+11.12.06.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiqIuS6d_yBrrLyuFUETwzdQcbNzdks0a_tZDyZIwUyUcLJzezzuXJD37C_MciDNT0ZPPAYDJQx8m_VDKtrTM9GSdOo-vWYKlOUhiYInY_Quw0iKN_j3txgGs7F7UvPeFMiQI2ikIXerdA/s1600/Screen+Shot+2014-05-02+at+11.12.06.png)

Download it, and expand it.  then take the complete eclipse folder and drop it into your /Applications folder.  It'll look like this.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXb_0C1uC-ZbIFlfRUu4e5x44S7Ek-xALkr2CB-w-YMLf0_DcjetSNAarWzM5nfnM2-yvxLEZKgBqAjGsOGK3YkRMXE2DdKnDwrCUZ1VFi8d_LeL1fgIMPDC7lo1nBVGc11vjEn0OvN5A/s1600/Screen+Shot+2014-05-02+at+11.21.03.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXb_0C1uC-ZbIFlfRUu4e5x44S7Ek-xALkr2CB-w-YMLf0_DcjetSNAarWzM5nfnM2-yvxLEZKgBqAjGsOGK3YkRMXE2DdKnDwrCUZ1VFi8d_LeL1fgIMPDC7lo1nBVGc11vjEn0OvN5A/s1600/Screen+Shot+2014-05-02+at+11.21.03.png)

Also, when you click on the Launcher, you'll see eclipse added to the list of applications.

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEil2j2Rnp5jkS8W_apOHpLJIgPFFmGcwY-044yF-Yxydtj1t-QxjRVzL0jPBI2JQDaB1ZESerH6LYzPySMtDlCje6rzhoc-5rcNgM6tUMkmhHR-ujUGfQeB48zDJmnWUmflh5TW-rC1nPc/s1600/Screen+Shot+2014-05-02+at+11.21.15.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEil2j2Rnp5jkS8W_apOHpLJIgPFFmGcwY-044yF-Yxydtj1t-QxjRVzL0jPBI2JQDaB1ZESerH6LYzPySMtDlCje6rzhoc-5rcNgM6tUMkmhHR-ujUGfQeB48zDJmnWUmflh5TW-rC1nPc/s1600/Screen+Shot+2014-05-02+at+11.21.15.png)

Now, When you run it, you may be asked if you want to install java 1.6 to run Eclipse.  Accept the install and sit back until it completes.  When its installed, you'll be able to run eclipse, so click the icon in the launcher, as above.

Eclipse will appear like this below.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgLPIfn4HFcibD8BiRhg8NylvBaVeDgvAgOWSjwz03sC5vP4yQed8MBaHt4BhQlrbT1aKPzohEHyyfZ0HTt0kzNk4G7wl0xHfdTXSFkhQJ4B-YUINVbCfXgRfA0J7_rW9olasiPkw7bfyI/s1600/Screen+Shot+2014-05-02+at+11.29.36.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgLPIfn4HFcibD8BiRhg8NylvBaVeDgvAgOWSjwz03sC5vP4yQed8MBaHt4BhQlrbT1aKPzohEHyyfZ0HTt0kzNk4G7wl0xHfdTXSFkhQJ4B-YUINVbCfXgRfA0J7_rW9olasiPkw7bfyI/s1600/Screen+Shot+2014-05-02+at+11.29.36.png)

We'll want to see what java versions we have installed and for that you can go to preferences and type jdk into the filter box which will show a number of java related options.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXUBMA6FSrh7m7NiWsJrvhZqSsMGaElcczCGrojXRBBm-SUGsxZ5QmS3yvg5YH_PxEcsFlxxT2X5z6JTKYbrkvfc6E5yht4ozBon8R-sr-BNV80f84AYJLhfWfn5cuZZ2ozfPWNGi4fn0/s1600/Screen+Shot+2014-05-02+at+11.32.52.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXUBMA6FSrh7m7NiWsJrvhZqSsMGaElcczCGrojXRBBm-SUGsxZ5QmS3yvg5YH_PxEcsFlxxT2X5z6JTKYbrkvfc6E5yht4ozBon8R-sr-BNV80f84AYJLhfWfn5cuZZ2ozfPWNGi4fn0/s1600/Screen+Shot+2014-05-02+at+11.32.52.png)As you can see, we have a preference called installed JRE's which, when we click on it will only have the apple JDK we installed when we first tried to start eclipse.  I want [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and [JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) and I got them on the oracle site for Java.  Download both dmg files from Oracle, double click them and follow the instructions on the installer to drop them in.  If you restart eclipse, and go back to the preferences, to this page you will now see the appropriate JDKs installed and you can choose your default for your project.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_9JwhatqK9pg_O92zRzUEn2uE8Ld7_-tVkbTD-B8m8RQQkHBmJSjUkjz-n-hRlaKogKRnZl4PY3BFB7y-Hxd7a_EYXBt8GJNX77IWzbc0otYGAa4qcvRT3tMlxhe5g4C2cMpHvz2bF54/s1600/Screen+Shot+2014-05-02+at+11.39.21.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_9JwhatqK9pg_O92zRzUEn2uE8Ld7_-tVkbTD-B8m8RQQkHBmJSjUkjz-n-hRlaKogKRnZl4PY3BFB7y-Hxd7a_EYXBt8GJNX77IWzbc0otYGAa4qcvRT3tMlxhe5g4C2cMpHvz2bF54/s1600/Screen+Shot+2014-05-02+at+11.39.21.png)

Now, part two.  Getting subversion into your eclipse, which turns out to be kinda difficult when you are trying to figure out which path to do.  There are various schools of thought on how to get subversion on to your mac, but for me so far, I have found Brew to be one of the best of the latest package installers out there.  If you do not have Brew installed you can do that really quickly by running this command in a terminal window.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi-ixe1G17PC6Z02gStey8lCyO6laNA7iTxn6JKUp3tRornyHau7NvvvqCjunNOzym-S1HSZjH_F3xg94Mp-3fzHWzOIE04RP5j8s-5g9gUR6hM7C58YqPiIUY9-wZWhGraXHro_RFU2VM/s1600/Screen+Shot+2014-05-02+at+11.45.07.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi-ixe1G17PC6Z02gStey8lCyO6laNA7iTxn6JKUp3tRornyHau7NvvvqCjunNOzym-S1HSZjH_F3xg94Mp-3fzHWzOIE04RP5j8s-5g9gUR6hM7C58YqPiIUY9-wZWhGraXHro_RFU2VM/s1600/Screen+Shot+2014-05-02+at+11.45.07.png)

which gets you this output.

```
lisas-MacBook-Air:~ bamcgill$ ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go/install)"
==> This script will install:
/usr/local/bin/brew
/usr/local/Library/...
/usr/local/share/man/man1/brew.1

Press RETURN to continue or any other key to abort
==> /usr/bin/sudo /bin/chmod g+rwx /Library/Caches/Homebrew
==> Downloading and installing Homebrew...
remote: Counting objects: 169292, done.
remote: Compressing objects: 100% (47341/47341), done.
remote: Total 169292 (delta 120836), reused 169278 (delta 120826)
Receiving objects: 100% (169292/169292), 32.51 MiB | 121 KiB/s, done.
Resolving deltas: 100% (120836/120836), done.
From https://github.com/Homebrew/homebrew
 * [new branch]      master     -> origin/master
HEAD is now at 23e1c24 ansible: fix --HEAD install
==> Installation successful!
You should run `brew doctor' *before* you install anything.
Now type: brew help
lisas-MacBook-Air:~
```

Badda Bing. Now, we can install subversion from the Brew repository and as all homebrew experts know, you keep your home-brews in the Cellar, so look out for /usr/local/Cellar appearing.   Now you may be asked for your administrator passwords as you do this because brew setups up the Cellar under /usr/Local and needs to create that there if it does not exist and set the permissions on the directory.  
Next, we'll want to install subversion with Brew.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgGDjLMCa5tQCwKfExeqYVn0Vj8oVAhyum0VMuMzWShkgGEdMoM4GUbagmaXGxOG87PsWUtzi3U6YDxS0aiWbKeQ9A3IrsRYKU2PWTWfEAFuGzZBqby6pyZS2qgySeu4S7uKv7Dr7qL99o/s1600/Screen+Shot+2014-05-02+at+12.14.23.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgGDjLMCa5tQCwKfExeqYVn0Vj8oVAhyum0VMuMzWShkgGEdMoM4GUbagmaXGxOG87PsWUtzi3U6YDxS0aiWbKeQ9A3IrsRYKU2PWTWfEAFuGzZBqby6pyZS2qgySeu4S7uKv7Dr7qL99o/s1600/Screen+Shot+2014-05-02+at+12.14.23.png)

This will install subversion and its dependencies for you.

Now, lastly, you'll need to install SVN support on eclipse.  The best one I've seen and have been using for ages has been [Subclipse from Tigris.org](http://subclipse.tigris.org/). If you go to the [download page](http://subclipse.tigris.org/servlets/ProjectProcess?pageID=p4wYuA), you'll see some notes on the download pages and sections for each release like this

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi0SbFPesiO8FSrdRxbILa_CKCegx6KIBsSjMGptlTasApC4OqnRRZGZq4DnGF0I8aPqV0Ociw-voOhQcjtd5OdcOFsoExLihhq5_0BCgclSgIRU2eXhXV7MbzsMwdLX_RVsbFQume0J8M/s1600/Screen+Shot+2014-05-02+at+12.18.24.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi0SbFPesiO8FSrdRxbILa_CKCegx6KIBsSjMGptlTasApC4OqnRRZGZq4DnGF0I8aPqV0Ociw-voOhQcjtd5OdcOFsoExLihhq5_0BCgclSgIRU2eXhXV7MbzsMwdLX_RVsbFQume0J8M/s1600/Screen+Shot+2014-05-02+at+12.18.24.png)

What we want to pick up is the Eclipse update Site URL. We can then take that and use it in eclipse to install subclipse for us.   
So. Open eclipse again and go to HELP > Install New Software  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiiRs_6J_rqfvMnjUXo7TiNqj5KiNm0tPslDE_FzjEG2Kp1AGr1fFtkOaOOPgmfu10V2zZMVFKvF-fpUNqwC7SVCJgFhP07v3aPhIYfRmQOnbILQ5lGbzUw2E_bufQY1tKopDA-mKqDgGs/s1600/Screen+Shot+2014-05-02+at+12.20.56.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiiRs_6J_rqfvMnjUXo7TiNqj5KiNm0tPslDE_FzjEG2Kp1AGr1fFtkOaOOPgmfu10V2zZMVFKvF-fpUNqwC7SVCJgFhP07v3aPhIYfRmQOnbILQ5lGbzUw2E_bufQY1tKopDA-mKqDgGs/s1600/Screen+Shot+2014-05-02+at+12.20.56.png)

This will popup the window below for available software and if you use the drop box, you'll see things like eclipse and myln and other update sites which base eclipse uses.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj4Qy8WQ4pm-e0OQCJ3978bMzNfhCzkQTr_66_RNWUi7BGPzM8M5UNIOagtOZnZQu9aB7a8hijdlC1hibHoqI9wgEvbhCJYhPraeNQj1yKOJd52oAa-QmO_IdF4fbQmPPz9bjDRFGSIdtc/s1600/Screen+Shot+2014-05-02+at+12.21.51.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj4Qy8WQ4pm-e0OQCJ3978bMzNfhCzkQTr_66_RNWUi7BGPzM8M5UNIOagtOZnZQu9aB7a8hijdlC1hibHoqI9wgEvbhCJYhPraeNQj1yKOJd52oAa-QmO_IdF4fbQmPPz9bjDRFGSIdtc/s1600/Screen+Shot+2014-05-02+at+12.21.51.png)

 We need to add another for Subclipse.  Remember we grabbed the update url from the Subclipse site, we can add a new site by clicking add and pasting in the URL and a name for the site as shown.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiX0AJoWOchNSYDnC7qW36Ir5jpCRdNBq46iDo16IpmgkYzD1bFc_jaIJtnSpTGqiIXoKKbElNsDzGqZdSLjfT6OqA_YnclHadquQxUwJohya-o51bGSJ4-DZz-ku-DNveRVRMyHNSko5I/s1600/Screen+Shot+2014-05-02+at+12.22.28.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiX0AJoWOchNSYDnC7qW36Ir5jpCRdNBq46iDo16IpmgkYzD1bFc_jaIJtnSpTGqiIXoKKbElNsDzGqZdSLjfT6OqA_YnclHadquQxUwJohya-o51bGSJ4-DZz-ku-DNveRVRMyHNSko5I/s1600/Screen+Shot+2014-05-02+at+12.22.28.png)

 This will appear like this and will give you the options that below to install subclipse and the SVNKit.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhKCO3ZYmlFvd5HWIsoiY9aExBVuToBrFkWuZoqBZRL2gXlurNX29FFxLq_KCzwh-heIr8EmY0ac0jcdbM4jEPjfJ2Y8oAM1ZbKVnQZyQep_utcW6I_C-WzqJuFWNCoC_VCAibQYOGaywI/s1600/Screen+Shot+2014-05-02+at+12.23.20.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhKCO3ZYmlFvd5HWIsoiY9aExBVuToBrFkWuZoqBZRL2gXlurNX29FFxLq_KCzwh-heIr8EmY0ac0jcdbM4jEPjfJ2Y8oAM1ZbKVnQZyQep_utcW6I_C-WzqJuFWNCoC_VCAibQYOGaywI/s1600/Screen+Shot+2014-05-02+at+12.23.20.png)

  
Install these and its normally good to restart eclipse after these installs.  The last thing you need to do then is to make sure you are using the right svnkit in eclipse once you restart.  
You can make sure of this by going to the preferences again and searching for SVN.  Click on the main SVN preference and make sure the SVN interface is set to SVNKit instead of javaHL.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgveDGx95dpzJwkvJ-eBW0DAfHo6VNjWj3j5uPDFSf5FWbxXYnpC6SOvI8xo4QEiUyuPFnZEG3gk-uQcVDGiJV_SicrT5744ALQJQp8yB3lfUg5NshEgqccEjqqYzmodyzfcc3qYn4cKnY/s1600/Screen+Shot+2014-05-02+at+16.35.03.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgveDGx95dpzJwkvJ-eBW0DAfHo6VNjWj3j5uPDFSf5FWbxXYnpC6SOvI8xo4QEiUyuPFnZEG3gk-uQcVDGiJV_SicrT5744ALQJQp8yB3lfUg5NshEgqccEjqqYzmodyzfcc3qYn4cKnY/s1600/Screen+Shot+2014-05-02+at+16.35.03.png)

Now, svn should be all set up and you can go look at adding new repositories and checking out code.
