---
title: 'MySQL 事务隔离级别与 MVCC'
description: '为什么 RR 能实现可重复读，而 RC 不能？实现原理是什么？'
pubDate: 'May 3 2026'
heroImage: '../../assets/blog-placeholder-3.jpg'
---

# MySQL 事务隔离级别与 MVCC

## 为什么 RR 能实现可重复读，而 RC 不能？实现原理是什么？

### ① 什么是 MVCC？

Multiversion Concurrency Control，多版本并发控制。

是一种用来解决读-写冲突的无锁并发控制。

为事务分配单向增长的时间戳，为每次修改保存一个版本，版本与事务时间戳关联。

读操作只读该事务开始前的数据库快照。

### ② 快照读与当前读

- **快照读**：读取数据的快照版本，不用加锁，如 select。
- **当前读**：读取数据的最新版本，如 insert、update、delete、select for update。

### ③ 隐藏字段、Undo Log、Read View

**InnoDB 每个聚簇索引记录都有隐藏字段：**
- `DB_ROW_ID`：行ID
- `DB_TRX_ID`：事务ID  
- `DB_ROLL_PTR`：回滚指针

**Undo Log：**
- 存储的是老版本数据
- 当事务回滚时，可以通过回滚指针回滚
- 当事务提交后，Undo Log 会被清理

**Read View：**
- 记录 Read View 创建时所有活跃事务列表
- `trx_ids`：当前活跃的事务ID集合
- `min_trx_id`：最小活跃事务ID
- `max_trx_id`：创建 Read View 时最大事务ID（递增）
- `creator_trx_id`：创建者的事务ID

### ④ RC 与 RR 的区别

- **RC**：每次读取都生成新的 Read View，所以能读到其他事务提交的最新数据
- **RR**：只在第一次读取时生成 Read View，后续复用，所以能实现可重复读

关键区别在于 **Read View 的生成时机**不同。
