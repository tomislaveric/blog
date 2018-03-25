---
layout: default
title:  "Git cheetsheat with some nice and useful commands"
categories: cheatsheets git
---
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
//Show nice git history overview
git log --all --decorate --oneline --graph
{% endhighlight %}