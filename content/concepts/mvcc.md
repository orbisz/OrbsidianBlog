---
title: MVCC (Multi-Version Concurrency Control)
category: concepts
tags: [database, MySQL, concurrency, isolation]
sources: ["F:/blog/my-blog/blogs/backend/MVCC.md"]
summary: MVCC 多版本并发控制，通过为每个数据行维护多个版本来实现事务隔离。核心依赖 Read View、undo log 和隐藏字段，详解数据可见性算法及 RC/RR 隔离级别的差异。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.75
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.85
  inferred: 0.10
  ambiguous: 0.05
---

# MVCC (Multi-Version Concurrency Control)

MVCC 是一种并发控制机制，通过在每个数据行上维护多个版本的数据来实现事务隔离。当事务修改数据时，MVCC 创建数据快照而非直接修改实际数据行。

## 核心组件

### 隐藏字段
- **DB_TRX_ID** (6字节): 最后一次插入或更新该行的事务 ID。（delete 被视为更新，标记 deleted_flag）
- **DB_ROLL_PTR** (7字节): 回滚指针，指向 undo log
- **DB_ROW_ID** (6字节): 无主键时 InnoDB 自动生成的聚簇索引 ID

### Read View

用于可见性判断，包含四个字段：
- **m_low_limit_id**: 当前最大事务 ID+1，>= 此 ID 的版本不可见
- **m_up_limit_id**: 活跃事务列表中最小 ID，< 此 ID 的版本可见
- **m_ids**: Read View 创建时未提交的活跃事务 ID 列表
- **m_creator_trx_id**: 创建该 Read View 的事务 ID

### undo log
- **insert undo log**: insert 操作产生，事务提交后可直接删除
- **update undo log**: update/delete 操作产生，提交后放入链表等待 purge 线程清理

## 数据可见性算法

逐行判断 DB_TRX_ID 与 Read View 的关系：

1. `DB_TRX_ID < m_up_limit_id` → 可见
2. `DB_TRX_ID >= m_low_limit_id` → 不可见，沿 DB_ROLL_PTR 回溯
3. `m_ids == 空` → 可见
4. `m_up_limit_id <= DB_TRX_ID < m_low_limit_id`:
   - 在 m_ids 中能找到 → 不可见
   - 找不到 → 可见
5. 不可见时沿 undo log 链回溯，重复判断

## RC vs RR 隔离级别差异

- **RC (Read Committed)**: 每次 SELECT 前生成新的 Read View
- **RR (Repeatable Read)**: 仅在该事务第一次 SELECT 前生成 Read View（默认隔离级别）

## 相关页面
- [[concepts/mysql-fundamentals]] — MySQL 基础
