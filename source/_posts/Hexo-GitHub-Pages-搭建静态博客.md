---
title: Hexo + GitHub Pages 搭建静态博客
date: 2018-04-01 16:16:16
tags: Hexo
---

## 什么是 Hexo？

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

## 搭建步骤

- GitHub 创建个人仓库
- 安装 Git
- 安装 Node.js
- 安装 Hexo
- 建站、关联 GitHub<!--more-->

**GitHub 创建个人仓库**

在自己的 GitHub 账号下创建一个新的空的仓库，命名为`username.github.io`（其中 username 是自己的账号名)。

**安装 Git**

根据操作系统安装 Git，配置 name 和 email 属性，生成 ssh 密钥文件，将公钥添加到 GitHub 的 Settings 中。

**安装 Node.js**

根据操作系统到官网下载对应安装包，安装 Node.js ，并将启动路径添加到环境变量中。

**安装 Hexo**

```shell
npm install -g hexo-cli 
```

**建站、关联 GitHub**

```shell
hexo init <folder>
cd <folder>
npm install
npm install hexo-deployer-git
```

修改配置文件 _config.yml：

```
deploy:
  type: git
  repo: git@github.com:username/username.github.io.git
  branch: master
```

至此，建站基本完成，为了更方便在不同电脑上迁移博客，于是使用 GitHub 存放生成的网站原始文件：

```shell
git init
git checkout -b hexo
git add --all
git commit -m 'new branch hexo'
git remote add origin git@github.com:username/username.github.io.git
git push -u origin hexo
```

将当前文件夹初始化为一个 git 仓库，新建并切换到 hexo 分支，添加所有的文件，commit，建立与远程仓库的联系，推送到远程的 hexo 分支。设置 hexo 为默认分支（因为我们只需要手动管理这个分支上的 Hexo 网站文件）。

## 总结

至此，就完成了静态博客的搭建，实现了在 GitHub 上用 hexo 分支来存放生成的网站原始文件，master 分支来存放生成的静态文件。

关于日常改动的流程：

1. 执行 `hexo g -d` 发布网站到 master 分支上；
2. 然后再依次执行 `git add`、`git commit -m "..."`、`git push origin hexo` 指令，将改动推送到 GitHub（当前应处于 hexo 分支）。

换电脑后的流程：

1. 拷贝仓库（默认分支为 hexo ）；
2. 在本地新拷贝的文件夹下依次执行下列指令：`npm install`、`npm install hexo-deployer-git`（note: 不需要`hexo init`这条指令）。