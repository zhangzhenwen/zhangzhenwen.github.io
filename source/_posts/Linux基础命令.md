---
title: Linux 基础命令
author: 张振文
avatar: 'https://cdn.jsdelivr.net/gh/ZhangZhenwen/cdn@1.0.0/img/custom/avatar.jpg'
authorLink: 'https://www.zhenwen66.cn'
authorAbout: 一个好奇的人
authorDesc: 一个好奇的人
categories: 技术
comments: true
date: 2020-07-23 22:31:01
tags:
 - 悦读
 - Linux
keywords: Linux
description: 
photos: https://i.loli.net/2020/07/25/7D8vxaQMlsbAYEZ.jpg
---

## Linux 基础命令

### 命令格式





### 目录处理命令

#### 1、mkdir 创建新目录

英文：make directories

所在路径：/bin/mkdir

权限：所有用户

语法：mkdir -p [目录名]

​						-p 递归创建

#### 2、cd 切换目录

英文：change directories

所在路径：shell 内置命令

权限：所有用户

语法：cd [目标目录]

#### 3、pwd 显示当前目录

英文：print working directory

所在路径：/bin/pwd

权限：所有用户

语法：pwd

#### 4、rmdir 删除空目录

英文：remove empty directories

所在路径：/bin/rmdir

权限：所有用户

语法：rmdir [目录名]

#### 5、cp 复制文件或目录

英文：copy

所在路径：/bin/cp

权限：所有用户

语法：cp -rp [原文件或目录] [目标目录]

​				  -r 复制目录

​				  -p 保留文件属性

#### 6、mv 剪切文件，改名

英文：move

所在路径：/bin/mv

权限：所有用户

语法：mv [原文件或目录] [目标目录]

7. rm 删除文件

   英文：remove

   所在路径：/bin/rm

   权限：所有用户

   语法：rm -rf [文件或目录]

   ​                   -r 删除目录

   ​                   -f 强制执行



### 文件处理命令

#### 1、touch 创建空文件

所在路径：/bin/touch

权限：所有用户

语法：touch [文件名]

#### 2、cat 显示文件内容

所在路径：/bin/cat

权限：所有用户

语法：cat -n [文件名]

​				  -n 显示行号

#### 3、tac 显示文件内容（反向排列）

所在路径：/usr/bin/cat

权限：所有用户

语法：tac -n [文件名]

​				  -n 显示行号

#### 4、more 分页显示文件内容

所在路径：/bin/more

权限：所有用户

语法：more [文件名]

​			(空格) 或 f 下一页

​			b                上一页

​			(Enter)	   换行

​			q 或 Q	    退出

#### 5、less 分页显示文件内容（向上翻页）

所在路径：/bin/less

权限：所有用户

语法：less [文件名]

#### 6、head 显示文件前几行

所在路径：/bin/head

权限：所有用户

语法：head -n 10 [文件名]

​					  -n 指定行数

#### 7、tail 显示文件后几行

所在路径：/bin/tail

权限：所有用户

语法：tail -n 10 [文件名]

​				  -n 指定行数

​				  -f  动态显示文件末尾内容



### 链接命令

#### ln 生成链接文件

英文：link

所在路径：/bin/ln

权限：所以用户

语法：ln -s [原文件] [目标文件]

​				-s 创建软链接（快捷方式）

硬连接特征

1. cp -p + 同步更新
2. 通过 i 节点识别
3. 不能跨分区
4. 不能针对目录使用



### 权限管理命令

#### 1、chmod 修改文件或目录权限

英文：change the permissions mode of a file

所在路径：/bin/chmod

权限：所有用户

语法：chmod [{ugoa} {+-=} {rwx}] [文件或目录]

​						 [mode = 421] [文件或目录]

​						 -R 递归修改

<img src="https://i.loli.net/2020/07/24/3s5qGEh9zVWmHaA.png" style="zoom:80%;" />

#### 2、chown 修改文件或目录的所有者

英文：change file ownership

所在路径：/bin/chown

权限：所有用户

语法：chown [用户] [文件或目录]

#### 3、chgrp 修改文件的所属组

英文：change file group ownership

语法：chgrp [用户组] [文件或目录]

#### 4、umask 显示、设置文件的缺省权限

英文：the user file-creation mask

路径：shell 内置命令

语法：umask [-S]

​						  -S 以 rwx 形式显示新建文件缺省权限



### 文件搜索命令

#### 1、find 文件搜索

语法：find [搜索范围] [匹配条件]

​					-name 根据名称

​					-iname （不区分大小写）

​					-size 根据大小 +n 大于 -n 小于 n 等于

​					-user 根据所有者

​					-group 根据所属组

​					-amin 访问时间

​					-cmin 文件属性

​					-mmin 文件内容

​					-a 两个条件同时满足

​					-o 两个条件满足一个

​					-type 根据文件类型

​					-inum 根据 i 节点

​					-exec/-ok [命令] {} \; 对搜索结果执行操作 （-ok 需要确认）

#### 2、locate 文件资料库中查找文件

所在路径：/usr/bin/locate

语法：locate [文件名]

#### 3、which 搜索命令所在位置及别名信息

所在路径：/usr/bin/which

语法：which 命令

#### 4、whereis 搜索命令所在位置及帮助文档路径

所在路径：/usr/bin/whereis

语法：whereis 命令

#### 5、grep 在文件中搜寻字串匹配的行

所在路径：/bin/grep

语法：grep -iv [指定字串] [文件]

​					 -i 不区分大小写

​					 -v 排除指定字串



### 帮助命令

#### 1、man 获得帮助信息

英文：manual

所在路径：/usr/bin/man

语法：man [命令或配置文件]

#### 2、help 获取 shell 内置命令的帮助信息

所在路径：shell 内置命令

语法：help [命令]



### 用户管理命令

#### 1、useradd 添加新用户

所在路径：/usr/sbin/useradd

权限：root

语法：useradd 用户名

#### 2、passwd 设置用户密码

所在路径：/usr/bin/passwd

语法：passwd 用户名

#### 3、who 查看登录用户信息

所在路径：/bin/who

语法：who

#### 4、w 查看登录用户详细信息

所在路径：/usr/bin/w

语法：w



### 压缩解压命令

#### 1、gzip 压缩文件

所在路径：/bin/gzip

语法：gzip [文件]

#### 2、gunzip 解压 .gz 的压缩文件

所在路径：/bin/gunzip

语法：gunzip [压缩文件]

#### 3、tar 打包目录

所在路径：/bin/tar

语法：tar [-zcf] [压缩后文件名] [目录]

​					-c 打包

​					-v 显示详细信息

​					-f 指定文件名

​					-z 打包同时压缩/解压缩

​					-x 解包

#### 4、zip 压缩文件或目录

所在路径：/usr/bin/zip

语法：zip [-r] [压缩后文件名] [文件或目录]

​					-r 压缩目录

#### 5、unzip 解压 .zip 文件

所在路径：/usr/bin/unzip

语法：unzip [压缩文件]

#### 6、bzip2 压缩文件

所在路径：/usr/bin/bzip2

语法：bzip2 [-k] [文件]

​						-k 保留原文件

​			tar -xjf [文件]

#### 7、bunzip2 解压 .bz2 文件

所在路径：/usr/bin/bunzip2

语法：bunzip2 [-k] [压缩文件]

​							-k 保留原文件

​			tar -xjf [压缩文件]



### 网络命令

#### 1、write 给用户发信息

所在路径：/usr/bin/write

语法：write 用户名

​			ctrl + D 保存结束

#### 2、wall 发广播信息

英文：write all

所在路径：/usr/bin/wall

语法：wall [message]

#### 3、ping 测试网络连通性

所在路径：/bin/ping

语法：ping [-c] ip地址

​					  -c 指定发送次数

