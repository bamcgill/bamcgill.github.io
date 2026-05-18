---
title: "Making Git cmd line fancy - ish :)"
date: 2018-04-27 17:44:00 +0000
last_modified_at: 2018-04-27 17:44:06 +0000
tags:
  - open source
  - git
  - oracle
  - bash
---

So, we're having a great time with git, fighting over how branches should work and what policy is best in our environment, which I suppose I'll talk about in another post, but for today, I wanted to share a little bit of usefulness.  
  
Most of our repositories have several branches for various releases and its often confusing and terse to 1. remember where you are and 2, run git branch to see.   
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhTDBmqdpkJw3c4lzG72-ZD9SP9M_sw8zLl3I7Jr_u3hRVQ2TTTsactgquoePWojgegt9RE6v9KQsrrGWxI6v4AxfjhgZSu8VbsJuRT2gTG6JB64X5ovVTYrT-90ADzwePyUtjvDNQx10U/s640/Screen+Shot+2018-04-27+at+18.18.30.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhTDBmqdpkJw3c4lzG72-ZD9SP9M_sw8zLl3I7Jr_u3hRVQ2TTTsactgquoePWojgegt9RE6v9KQsrrGWxI6v4AxfjhgZSu8VbsJuRT2gTG6JB64X5ovVTYrT-90ADzwePyUtjvDNQx10U/s1600/Screen+Shot+2018-04-27+at+18.18.30.png)

This for example, I have changed to my repository in GitHub, but unless you know that you're in a repository you couldn't be sure.  Long story short, lets say we've had one or two boo-boos along the way.

Now, imported projects in eclipse will have the branch of the code you're working on so today, we're going to bring it to the terminal.  Cut the following and put it in your .bashrc or .bash\_profile and see your repository and branch pop out on the prompt.  Now,  I have decorated the prompt with some colours, which you might want to change.  (search for bash unix colors for details)

parse\_git\_branch() {

git branch 2> /dev/null | sed -e '/^[^\*]/d' -e 's/\* \(.\*\)/[\1]/'

}

parse\_git\_repo() {

git rev-parse --show-toplevel 2> /dev/null | xargs basename| sed 's/\(.\*\)/[\1]/'

}

export PS1="\[\033[91m\]\u\[\033[30m\]@\[\033[34m\]\h[\[\033[36m\]\w\[\033[30m\]] \

\n\r\[\033[31m\]\$(parse\_git\_repo)\[\033[00m\]-\[\033[33m\]\$(parse\_git\_branch)\[\033[00m\] $ "

What you get from all this, the next time you start a terminal is this (without my adornments).

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYwGUpeEJ-SmnD6WL_G32DH2bgMfHP39BX413mAxNtmsr66cl-JbXDH89wb04rpWyFKGeIT78TUPNHPAfuNLa3TAP2eJWJkrlXhkgZ5ASakBjOnoHb3RtjLucFy_VYFH1sOPKZVg-VDAA/s640/Screen+Shot+2018-04-27+at+18.29.10.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYwGUpeEJ-SmnD6WL_G32DH2bgMfHP39BX413mAxNtmsr66cl-JbXDH89wb04rpWyFKGeIT78TUPNHPAfuNLa3TAP2eJWJkrlXhkgZ5ASakBjOnoHb3RtjLucFy_VYFH1sOPKZVg-VDAA/s1600/Screen+Shot+2018-04-27+at+18.29.10.png)

So, as soon as you enter a repository, the prompt now tells you which repository and which branch you are on too, in this case I have branch called flatten which I used for the previous post.

Finally, if you dont want the colour, strip the escape codes and while your PS1 export will look more sane, it'll lack a certain bedazzling...

export PS1="\u@\h[\w] \n\r\$(parse\_git\_repo)-\$(parse\_git\_branch) $ "

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhlklrURrt8lTEMw4ySN-QfPMOdMFo2l3r8w23VRfUtiPEn7om95vuensflnpusmdaUJ5JYItJNHNgZtX1Myr5tTNikH-Nmu3YMriKW9fTo0TqJ6VM9YWuDuVtB3Gr6v0mkjsYc2d0uAWg/s640/Screen+Shot+2018-04-27+at+18.42.13.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhlklrURrt8lTEMw4ySN-QfPMOdMFo2l3r8w23VRfUtiPEn7om95vuensflnpusmdaUJ5JYItJNHNgZtX1Myr5tTNikH-Nmu3YMriKW9fTo0TqJ6VM9YWuDuVtB3Gr6v0mkjsYc2d0uAWg/s1600/Screen+Shot+2018-04-27+at+18.42.13.png)

Have fun!
