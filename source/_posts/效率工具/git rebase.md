---
title: git rebase
tags:
  - Git
comments: false
date: 2019-04-27 19:26:45
categories: [效率工具,Git]
---

// rebase操作可以把本地未push的分叉提交历史整理成直线；

// rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
git checkout feature
git rebase master

#### cherry-pick只合并某次提交

使用该命令可以将任意的commit通过其commit号将其合并到你想要的分支上。

打开终端，在对应的分支号下操作：

git cherry-pick b36ef98（commit的哈希值）

当出现冲突：在项目中找到冲突，解决冲突，提交即可