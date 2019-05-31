---
title: git push
tags:
  - Git
comments: false
date: 2019-04-27 19:26:45
categories: [效率工具,Git]
---

```bash
//克隆项目
git clone https://github.com/baylin87/web-development-demo.git
```

```bash
//克隆某分支
git clone -b <branch-name> <git-address>
```

```bash
//进入项目目录
cd <name>
```

```bash
//查看git状态
git status
```

```bash
git add .
```

```bash
git commit -m "add Trtris and update readme"
```

```bash
git push -u origin master
```

如果push失败，则添加 `--force` 参数