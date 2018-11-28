+++
date = 2018-11-28
title= "Git cherry-pick from another repository"
Description = "Git cherry-pick from another repository"
Tags = ['git']
+++

Git 从其他代码库合并 commit 到当前代码库.

```bash
# Cloning your fork
$ git clone git clone git@github.com:your/repo.git

# Adding another repo that we want to cherry-pick
$ git remote add another git://github.com/another/repo.git

# Fetch their branches
$ git fetch another

# List their commits
$ git log another/master

# Cherry-pick the commit you need
$ git cherry-pick 123abc

# Pushing to your master
$ git push origin master
```
