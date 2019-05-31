---
title: git tag
tags:
  - Git
comments: false
date: 2019-04-27 19:26:45
categories: [效率工具,Git]
---

tag标签相当于版本库的快照

git tag //查看所有

git tag <tag-name> // 为当前分支commit打标签

git tag <tag-name> <commit id> // 为某次commit打标签

git show <tag-name> // 查看标签信息

git tag -d <tag-name> // 删除标签

git push origin --tags // 一次性推送全部尚未推送到远程的本地标签

git push origin <tagname> // 推送某个标签到远程，使用命令

git push origin :refs/tags/<tagname> //远程删除。删除命令也是push，但是格式如下：

注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。