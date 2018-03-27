---
layout: page
title:  "Git cheetsheat"
categories: cheatsheets git
---
A collection of git commands for you daily work.
{% highlight csharp %}
//Add all files you want to commit
git add . || git add singleFile
//Commit files with message
git commit -m "commit message"
//Create new branch and check it out
git branch -b branchName
//Merge branch develop into master
git checkout master && git merge develop
//Reset modified file
git checkout HEAD -- fileToReset
{% endhighlight %}

You can create a git alias for long git commands. Just add this, for example, to .gitconfig in HOME
{% highlight csharp %}
[alias]
    lg = log -n 20 --reverse --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
{% endhighlight %}
{% highlight csharp %}
//Short alias displays nice, colorful git history overview
git lg
{% endhighlight %}