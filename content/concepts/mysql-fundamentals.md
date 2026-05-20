---
title: MySQL 基础知识
category: concepts
tags: [MySQL, database, SQL, backend]
sources: ["F:/blog/my-blog/blogs/backend/mysql.md"]
summary: MySQL 关系型数据库基础知识，涵盖 DDL/DML/DQL/DCL 四类 SQL 语句、MySQL 架构分层及基本操作。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.70
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.85
  inferred: 0.10
  ambiguous: 0.05
---

# MySQL 基础知识

MySQL 是一个遵循关系模型的数据管理系统，通过"数据库 → 表 → 行 → 列"的层级结构组织数据，支持 ACID 事务特性。

## SQL 四类语句

### DDL (Data Definition Language) — 数据定义
`CREATE`, `ALTER`, `DROP`, `TRUNCATE` — 操作数据库和表结构

### DML (Data Manipulation Language) — 数据操作
`INSERT`, `UPDATE`, `DELETE` — 操作表中数据

### DQL (Data Query Language) — 数据查询
`SELECT` — 查询数据，最常用且最复杂

### DCL (Data Control Language) — 数据控制
`GRANT`, `REVOKE` — 权限管理

## MySQL 架构分层

- **连接层**: 连接处理、授权认证
- **服务层**: SQL 接口、解析器、优化器、缓存
- **引擎层**: 插件式存储引擎（InnoDB、MyISAM 等）
- **存储层**: 数据文件存储

## 相关页面
- [[concepts/mvcc]] — InnoDB MVCC 多版本并发控制
- [[concepts/redis-persistence]] — Redis 持久化
