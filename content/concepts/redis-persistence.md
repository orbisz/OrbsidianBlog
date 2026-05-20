---
title: Redis 持久化 — RDB 与 AOF
category: concepts
tags: [Redis, database, backend, persistence]
sources: ["F:/blog/my-blog/blogs/backend/RDBandAOF.md"]
summary: Redis 两种持久化机制对比：RDB（快照）和 AOF（追加日志）。涵盖工作原理、优缺点、混合持久化及实践选型建议。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.70
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.80
  inferred: 0.15
  ambiguous: 0.05
---

# Redis 持久化 — RDB 与 AOF

## RDB (Redis Database Backup)

按指定时间间隔生成数据快照保存到磁盘。

**触发方式**:
- `save` 命令（阻塞主线程）
- `bgsave` 命令（fork 子进程异步执行）
- 配置 `save <seconds> <changes>` 自动触发

**优缺点**:
- 优点: 文件紧凑，恢复速度快，适合灾难恢复
- 缺点: 可能丢失最后一次快照后的数据

## AOF (Append Only File)

以日志形式记录每次写操作命令。

**同步策略**:
- `appendfsync always`: 每条命令都 fsync，最安全但最慢
- `appendfsync everysec`: 每秒 fsync，推荐配置
- `appendfsync no`: 由操作系统决定

**AOF 重写**: 解决 AOF 文件膨胀问题，bgrewriteaof 异步重写。

## RDB vs AOF

| 维度 | RDB | AOF |
|---|---|---|
| 数据安全 | 可能丢数据 | 最多丢 1 秒 |
| 恢复速度 | 快 | 慢（重放命令） |
| 文件大小 | 小 | 大 |

**最佳实践**: 混合持久化（Redis 4.0+），RDB + AOF 结合，兼顾恢复速度和数据安全。

## 相关页面
- [[concepts/mvcc]] — MySQL 的持久性和事务
- [[concepts/mysql-fundamentals]] — MySQL 基础知识
