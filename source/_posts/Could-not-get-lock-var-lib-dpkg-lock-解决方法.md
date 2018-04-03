---
title: Could not get lock /var/lib/dpkg/lock, 解决方法
date: 2018-04-03 10:00:00
tags: Ubuntu
---

当执行`sudo apt-get XXX`这种命令时，出现类似下面的报错：

```shell
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
```

这是因为，还有一个进程在使用 **apt-get** 进行下载操作，此时解决方法是：

**找到并杀掉所有的 apt-get 和 apt 进程**<!--more-->

```shell
ps -A | grep apt
```

```shell
# sudo kill processnumber
sudo kill 1997
```

然后，关闭当前终端，再重新开一个终端，`sudo apt-get`命令就可以使用了。

**删除锁定文件**

锁定的文件会阻止 Linux 系统中某些文件或者数据的访问，一旦运行了 apt-get 或者 apt 命令，锁定文件将会创建于 `/var/lib/apt/lists/`、`/var/lib/dpkg/`、`/var/cache/apt/archives/` 中。

这有助于运行中的 apt-get 或者 apt 进程避免被其它需要使用相同文件的用户或者系统进程所打断。当该进程执行完毕后，锁定文件将会删除。

当没有看到 apt-get 或者 apt 进程的情况下，在上面的文件夹中看到了锁定文件，这是因为，进程由于某个原因被杀掉了，因此需要删除锁定文件来避免报错。

```shell
sudo rm /var/lib/dpkg/lock
```

```shell
sudo dpkg --configure -a
```

或者：

```shell
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
```

```shell
sudo apt-get update
```

