---
title: "Push the cloned repo to new empty repository"
output:
  html_document: default
date: "2024-10-17"
---


```{bash}
git clone https://github.com/JYLeeBioinfo/oldrepo.git
rm -rf .git # remove git history and information
git init # initialize
git add . # add all files to the tree
git commit # commit changes
git remote add origin https://github.com/JYLeeBioinfo/newrepo.git # set newrepo.git as new source
git push --set-upstream origin master # set master as origin
```