---
title: git提交规范
tags:
  - Git
comments: false
date: 2019-04-27 19:26:45
categories: [效率工具,Git]
---

作为一个git flow开发者，良好的commit书写习惯，能潜意识强化自身模块化开发并且通过commit快速定位代码。

> `git commit -m <本文描述内容>`


# 基本格式

```bash
<type>(<scope>): <subject>
```

## type

用于说明 commit 的类别，只允许使用下面7个标识。

1. feat：新功能（feature）
2. fix：修补bug
3. docs：文档（documentation）
4. style： 格式（不影响代码运行的变动）
5. refactor：重构（即不是新增功能，也不是修改bug的代码变动）
6. test：增加测试
7. chore：构建过程或辅助工具的变动

## scope

用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

## subject

是 commit 目的的简短描述，不超过50个字符。

1. 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
2. 第一个字母小写
3. 结尾不加句号（.）

# reference

- [阮一峰 --- Commit message 和 Change log 编写指南](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)