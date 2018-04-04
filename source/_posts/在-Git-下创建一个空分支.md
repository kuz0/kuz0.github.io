---
title: 在 Git 下创建一个空分支
date: 2018-04-04 20:20:20
tags: Git
---

有时候，我们需要在 Git 里面创建一个空分支，该分支不继承任何提交，没有父节点，完全是一个干净的分支，例如，我们需要在某个分支里存放项目文档。

使用传统的 **git checkout** 命令创建的分支是有父节点的，意味着新 branch 包含了历史提交，所以无法直接使用该命令。

## 解决方法

**使用 git checkout 的 --orphan 参数**：<!--more-->

```shell
git checkout --orphan doc
```

该命令会创建一个名为 doc 的分支，并且该分支下有前一个分支下的所有文件。

**删除当前所有内容，用 git 命令**：

```shell
git rm -rf .
```

**使用 commit 命令来提交分支**：

```shell
git commit -am "new branch for documentation"
```

如果没有任何文件提交的话，分支是看不到的，可以创建一个新文件后再次提交则新创建的 branch 就会显示出来。

**使用 branch 来查看分支是否创建成功**：

```shell
git branch -a
```

[Thx](https://segmentfault.com/a/1190000004931751)