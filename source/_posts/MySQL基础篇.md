---
title: MySQL 基础篇
author: 张振文
avatar: 'https://cdn.jsdelivr.net/gh/ZhangZhenwen/cdn@1.0.0/img/custom/avatar.jpg'
authorLink: https://www.zhenwen66.cn
authorAbout: 一个好奇的人
authorDesc: 一个好奇的人
categories: 技术
comments: true
date: 2020-07-17 22:40:27
tags:
 - 悦读
 - 数据库
 - MySQL
keywords:
description:
photos: https://i.loli.net/2020/07/18/LrUfeCFMNzoXyhi.jpg
---

## 一、基础架构：一条SQL语句是如何执行的？

下面是 MySQL 基础的架构示意图。

<img src="https://i.loli.net/2020/07/18/et5VhQRyHr3UYXp.png" alt="0d2070e8f84c4801adbfa03bda1f98d9" style="zoom: 33%;" />

​	大体来说，MySQL 可以分为 Server 层和存储引擎层两部分。

- Server层

  Server 层包括连接器、查询缓存、分析器、优化器、执行器等，涵盖 MySQL 的大多数核心服务功能，以及所有的内置函数（如日期、时间、数学和加密函数等），所有跨存储引擎的功能都在这一层实现，比如存储过程、触发器、视图等。

- 存储引擎层

  存储引擎层负责数据的存储和提取。其架构模式是插件式的，支持 InnoDB、MyISAM、Memeory 等多个存储引擎。最常用的是 InnoDB ，MySQL 5.5.5 之后默认存储引擎也是 InnoDB。

  不同存储引擎的表数据存取方式不同，支持的功能也不同。







