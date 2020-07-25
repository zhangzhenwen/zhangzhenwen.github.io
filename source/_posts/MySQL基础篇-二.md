---
title: MySQL 基础篇(二)
author: 张振文
avatar: 'https://cdn.jsdelivr.net/gh/ZhangZhenwen/cdn@1.0.0/img/custom/avatar.jpg'
authorLink: 'https://www.zhenwen66.cn'
authorAbout: 一个好奇的人
authorDesc: 一个好奇的人
categories: 技术
comments: true
date: 2020-07-20 17:43:35
tags:
 - 悦读
 - 数据库
 - MySQL
keywords: MySQL
description: 记录学习 MySQL 的笔记。该篇是基础篇(二)的内容，关于日志系统。
photos: https://i.loli.net/2020/07/21/qvoFrfQGd6bzlxn.png
---

## 日志系统：一条 SQL 更新语句是如何执行的？

首先，可以确定的说，查询语句的那一套流程，更新语句也是同样会走一遍。

<img src="https://i.loli.net/2020/07/18/et5VhQRyHr3UYXp.png" style="zoom: 33%;" />

与查询流程不一样的是，更新流程还涉及两个重要的日志模块，它们正是我们今天要讨论的主角：redo log（重做日志）和 binlog（归档日志）。

### 重要日志模块：redo log (InnoDB)

WAL 技术：Write-Ahead Logging 先写日志，再写磁盘。

当有一条记录要更新时，InnoDB 引擎会先把记录写到 redo log 里面，并更新内存。到适当时候，将这个操作记录更新到磁盘里面。

InnoDB 的 redo log 是固定大小的。例如一组4个文件，每个文件 1GB，就总共可以记录 4GB 内容。

<img src="https://i.loli.net/2020/07/20/PbyOGDBIMvNYRfZ.png" style="zoom:55%;" />

write pos：当前记录的位置，一边写一边后移，循环着写。

check pos：当前要擦除的位置，往后移，循环的。擦除前要把记录更新到数据文件中。

绿色部分就是 redo log 中还空着的部分，可以用来记录新的操作。当 write pos 追上 check pos，就不能执行新的操作，得擦除一些记录让 check pos 前进。

crash-safe：保证即使数据库发生异常重启，之前提交的记录都不会丢失的能力。

### 重要的日志模块：binlog

redo log 是 InnoDB 引擎特有的日志，而 Server 层也有自己的日志，称为 binlog (归档日志)。

binlog 日志只能用来归档，是没有 crash-safe 能力的。

这两个日志有三个不同点：

1. redo log 是 InnoDB 引擎特有的；binlog 是 MySQL 的 Server 层实现的，所有引擎都可以使用。
2. redo log 是物理日志，记录的是“在某个数据页上做了什么修改”；binlog 是逻辑日志，记录的是这个语句的原始逻辑，比如“给 ID=2 这一行的 c 字段加 1 ”。
3. redo log 是循环写的，空间固定会用完；binlog 是可以追加写入的。“追加写”是指 binlog 文件写到一定大小后会切换到下一个，并不会覆盖以前的日志。

有了对这两个日志的概念性理解，我们再来看执行器和 InnoDB 引擎在执行这个简单的 update 语句时的内部流程。

1. 执行器先找引擎取 ID=2 这一行。ID 是主键，引擎直接用树搜索找到这一行。如果 ID=2 这一行所在的数据页本来就在内存中，就直接返回给执行器；否则，需要先从磁盘读入内存，然后再返回。
2. 执行器拿到引擎给的行数据，把这个值加上 1，比如原来是 N，现在就是 N+1，得到新的一行数据，再调用引擎接口写入这行新数据。
3. 引擎将这行新数据更新到内存中，同时将这个更新操作记录到 redo log 里面，此时 redo log 处于 prepare 状态。然后告知执行器执行完成了，随时可以提交事务。
4. 执行器生成这个操作的 binlog，并把 binlog 写入磁盘。
5. 执行器调用引擎的提交事务接口，引擎把刚刚写入的 redo log 改成提交（commit）状态，更新完成。

<img src="https://i.loli.net/2020/07/21/PSdXYanlkp7mBFo.png" style="zoom:55%;" />

浅色框是在 InnoDB 中执行的，深色框是在执行器中执行的。

### 两阶段提交

redo log 的写入拆成了两个步骤：prepare 和 commit，这就是“两阶段提交”。为了让两份日志之间的逻辑一致。

想要数据库恢复到之前某一时刻，你可能会这么做：

- 首先，找到最近的一次全量备份，如果你运气好，可能就是昨天晚上的一个备份，从这个备份恢复到临时库
- 然后，从备份的时间点开始，将备份的 binlog 依次取出来，重放到中午误删表之前的那个时刻。

为什么日志需要“两阶段提交”。如果不使用“两阶段提交”会发生什么？

1. 先写 redo log 后写 binlog

   由于 redo log 和 binlog 是两个独立的逻辑，如果不用两阶段提交，假设在写完 redo log，binlog 还没写完的时候，MySQL 进程异常重启。由于 redo log 写完，系统崩溃，也能把数据恢复回来。

   但是 binlog 没写完就 crash 了，这时 binlog 没有这条更新的记录。之后备份日志，就没有这条语句。

   如果需要用这个 binlog 来恢复临时库的话，由于这个语句的 binlog 缺失，临时库就会少了这一次更新，与原库不同。

2. 先写 binlog 后写 redo log

   如果在 binlog 写完之后 crash，由于 redo log 还没写，崩溃恢复以后这个事务无效，所以这一行的值并没有改变。但是 binlog 里面已经记录了这个改变的日志。所以，在之后用 binlog 来恢复的时候就多了一个事务出来，与原库的值不同。

如果不使用“两阶段提交”，那么数据库的状态就有可能和用它的日志恢复出来的库的状态不一致。

当你需要扩容的时候，也就是需要再多搭建一些备库来增加系统的读能力的时候，现在常见的做法也是用全量备份加上应用 binlog 来实现的，这个“不一致”就会导致你的线上出现主从数据库不一致的情况。

简单说，redo log 和 binlog 都可以用于表示事务的提交状态，而两阶段提交就是让这两个状态保持逻辑上的一致。