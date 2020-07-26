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

## 文件处理命令

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



## 权限管理命令

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

#### 3、which 搜索命令所在位置



