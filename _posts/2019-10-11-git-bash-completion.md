---
title: "git bash completion"
date: 2019-10-11 15:15:00 +0000
last_modified_at: 2019-10-11 15:15:47 +0000
---

Try this in bash  
  
`git p`  
  
You get a file names p or a list of them.  Thats not much good, but there is a great bash completion library which you can source in your .bashrc to give you valid completion targets  
  
`$git p  
pull  
push  
$git p`  
  
Pull this [file](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash) and source it in your .bashrc  
  
  
`$wget https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash  
$echo . $PWD/git-completion.bash >> ~/.bashrc`  
  
Open up a new terminal window and enjoy.
