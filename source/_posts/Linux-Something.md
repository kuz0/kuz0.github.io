---
title: Linux Something
date: 2018-04-15 10:35:10
tags: Linux
---

## 1. Linux 常用命令

- ls (list) -a (all) -l (详细信息)
- cd (change directory)
- pwd (print work directory)
- mkdir (make directory) (-p abc/def)
- mv (move) pathname1 pathname2 (移动和重命名文件)
- touch pathname (创建空文件)
- cp (copy) pathname1 pathname2 -r (复制文件夹) -f (强制复制)
- rm (remove) pathname -r -f
- cat (直接在命令行中显示文件内容)
- rmdir (remove directory 删除空文件夹)
- ln (link 连接文件) 
- man (查询 man 手册)
- apt-get install / remove<!--more-->

## 2. Vi 使用

使用 Vi 来打开或创建一个文件：`vi pathname`

Vi 的两种模式：

- 命令模式：当 Vi 打开时，**默认为命令模式**，要转入输入模式，需要按 a 或者 i 键。在命令模式下，此时键盘上输入的所有东西都被 Vi 当作命令来对待。命令模式下最好不要乱输入，此时应输入相应的命令，来让 Vi 做相应的事。

- 输入模式：用来向文件输入内容。可以从命令模式中**按 a 或者 i 键进入输入模式**。进入输入模式后，就可以随意按键盘进行输入了。输入完成后如果要保存，要先退回到命令模式（因为保存也是一种命令）。在输入模式下**按 ESC 键退回到命令模式**。

  **注意看屏幕左下角**，当命令模式时，无提示信息或者提示文件名等信息，当处于输入模式时，提示 **-- INSERT --** 。

在命令模式下如何保存：

- :wq            保存并且退出
- :w            只保存不退出
- :q            不保存退出        进来看了一下没改退出
- :q!            不保存强制退出
- :wq!        保存并强制退出

查找、快速切换行、设置显示行号

- 查找 -- 在命令模式下，输入 /xxx，就可以查找到 xxx
- 快速切换行 -- 在命令模式下，输入 :num，就可以快速切换到 num 行
- 设置显示行号 -- 在命令模式下，输入 :set nu，就可以显示行号，输入 :set nonu，不显示行号
- 设置永久显示行号，需修改 Vi 配置文件。打开 Vi 配置文件 ~/.vimrc，输入 `set nu` 即可

行删除、行复制粘贴

- 行删除 -- 命令模式下，先将光标移动到要删除的行（或者 :n），然后输入 dd，如果要删除连续多行，譬如要删除连续的三行光标，则在三行的第一行，使用 3dd
- 行复制粘贴 -- 复制：命令模式下，nyy（3yy）-- 粘贴：命令模式下，p -- 细节，复制时要把光标放在多行的第一行，粘贴时实际粘贴到当前光标所在行的下一行。

## 3. 命令行中一些符号的含义

- .        代表当前目录
- ..        代表上一层目录，当前目录的父目录
- \-        代表前一个目录，刚才从哪个目录 cd 过来
- ~        代表当前用户的宿主目录
- /        代表根目录
- $        普通用户的命令行提示符
- \#        root用户的命令行提示符
- \*        万能匹配符   

## 4. Linux 高阶命令

- find

  功能：在 Linux 文件系统中，用来查找一个文件放在哪里。

  举例：find /etc -name "interfaces"

  总结：

  - 1> 什么时候用 find？

    当你知道你要找的文件名，但是忘记了它被放在哪个目录下，用 find。

  - 2> 怎么用 find ？

    find 路径 -name "文件名"

    find / -name "文件名"

- grep

  功能：在一个文本文件中，查找某个词。

  举例：grep -nr "SUN" *     （所有路径）

  ​	   grep -nr "SUN" 路径

  总结：

  - 1> 什么时候用 grep？

    当你想查找某个符号在哪些地方（有可能是一个文件，也有可能是多个文件组成的文件夹）出现过，就用 grep。

  - 2> 怎么用？

    grep -nr "要查找的符号" 要查找的目录或文件集合

    注意：-n表示查找结果中显示行号，-r表示要递归查找(文件夹里面也查)

- which 和 whereis

  功能：查找一个应用程序（二进制文件）在哪里

  举例：which ls         whereis ls

  区别：

  - which 只显示二进制文件的路径
  - whereis 显示二进制文件的路径，和其源码或 man 手册位置

- uname

  功能：查看系统信息

  举例：uname -a

- 开机和关机

  init 0                关机

  init 2             重启

  shutdown -h now    立即关机

  shutdown -r now    立即重启

  reboot                重启

- tree / lstree

  功能：显示文件和目录由根目录开始的树形结构

- mount / umount

  功能：用来挂载磁盘到文件系统中

  举例：mount -t nfs -o nolock 192.168.1.141:/root/rootfs /mnt    挂载

  umount /mnt 卸载

- 磁盘空间相关

  df -h    显示已挂载的分区列表，大小、容量

  du -h    列出文件或文件夹的大小

  du -h 文件名，可以列出这个文件有多大，列出方式是以人比较好看懂的方式。不像 ls -l 列出的都是以字节为单位。


- 用户管理

  useradd user1    添加一个名为 user1 的用户

  userdel user1    删除一个名为 user1 的用户

  passwd user1    为名为 user 的用户设置密码

  adduser user1    添加一个名为 user1 的用户，同时创建宿主目录，用户 shell 等。

  adduser 和 useradd 的区别：

  adduser 是一个脚本，而 useradd 是一个二进制应用程序。adduser 创建用户时比较麻烦，但是一次设定完所有的信息；而 useradd 设置时简单，但需要额外的设置宿主目录，密码那些信息。

- 权限管理

  作用：用来管理系统中文件的权限。

  chmod (change mode)

  chown (change owner) chown meng a.c

  chgrp (change group) chgrp meng a.c

  ls -l 列出的属性：-rwxr-xr-x

  一共十个字符，第一个表示文件属性（d 表示文件夹，- 表示普通文件），剩下的9个分成三组。每组中三个分别表示 r 可读 w 可写 x 可执行。如果是字母表示有这个权限，如果是 - 表示没这个权限。三组分别表示：第一组表示文件属主的权限，第二组表示属主所在的组用户的权限，第三组表示其他用户的权限。

  权限还有另一种表示方法，用数字来表示。

  编码规则如下：

  - r    可读        4
  - w    可写        2
  - \-    无权限        0
  - x    可执行        1

  有了这个编码规则，则 rwxr-xr-x  编码后为755

  第一种修改权限的方法：

  要把权限改成    rwxr--r--    则对应的编码值为744

  修改命令为：chmod 744 文件名

  第二种修改权限的方法：

  在原来的权限基础上进行修改，即增加或减少某权限。

  三个组用户的编码依次为： 属主u，属主所在的组g，其他用户o

  譬如

  要属主增加可执行权限    chmod u+x 文件名

  其他用户增加可写权限    chmod o+w 文件名

  属主所在组用户去掉可执行权限    chmod g-x 文件名

- 文件打包压缩与解压缩

  tar -czvf dir.tar.gz dir/        将dir目录打包成dir.tar.gz

  tar -cjvf dir.tar.bz2 dir/        将dir目录打包成dir.tar.bz2

  tar -zxvf dir.tar.gz             解压缩dir.tar.gz

  tar -jxvf dir.tar.bz2            解压缩dir.tar.bz2


- sed 和 awk

  正则表达式。匹配加替换。

- 格式化文件系统

  mkfs    /dev/hd1

  mkfs -t vfat 32 -F /dev/hd1        创建一个FAT32文件系统    

- 网络配置命令

  ifconfig eth0 192.168.1.13        设置IP地址

  ifconfig eth0 up                启动网卡

  ifconfig eth0 down                禁用网卡

  ifup eth0                        启动网卡

  ifdown eth0                        禁用网卡

  ifconfig eth0 192.168.1.1 netmask 255.255.255.0    同时设置IP和子网掩码


