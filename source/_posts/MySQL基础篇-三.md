---
title: MySQL 基础篇(三)
author: 张振文
avatar: 'https://cdn.jsdelivr.net/gh/ZhangZhenwen/cdn@1.0.0/img/custom/avatar.jpg'
authorLink: 'https://www.zhenwen66.cn'
authorAbout: 一个好奇的人
authorDesc: 一个好奇的人
categories: 技术
comments: true
date: 2020-07-21 00:50:33
tags:
 - 悦读
 - 数据库
 - MySQL
keywords: MySQL
description: 记录学习 MySQL 的笔记。该篇是基础篇(三)的内容，关于事务隔离。
photos: https://i.loli.net/2020/07/25/KL1ZUSaCn3wJqrW.jpg
---

## 事务隔离：为什么你改了我还看不见？

简单来说，事务就是要保证一组数据库操作，要么全部成功，要么全部失败。在 MySQL 中，事务支持是在引擎层实现的。你现在知道，MySQL 是一个支持多引擎的系统，但并不是所有的引擎都支持事务。比如 MySQL 原生的 MyISAM 引擎就不支持事务，这也是 MyISAM 被 InnoDB 取代的重要原因之一。

### 隔离性与隔离级别

