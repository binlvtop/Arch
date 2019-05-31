---
title: git merge
tags:
  - Git
comments: false
date: 2019-04-27 19:26:45
categories: [效率工具,Git]
---

//切换需要更新的分支
git checkout master

//从远程更新本地
git pull

//切换分支
git checkout 20180712-YUNDING-3469

//从master分支合并到当前分支
git merge master

// --no-ff 参数表示合并后的历史有分支，能看出来曾经做过合并
git merge --no-ff -m "merge with no-ff" dev

//查看git状态
git status

//从本地更新到远程
git push