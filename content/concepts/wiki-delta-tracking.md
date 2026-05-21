---
title: Wiki Delta Tracking
category: concepts
tags: [knowledge-management, incremental-processing, obsidian-wiki]
sources:
  - path: _raw/obsidian-wiki-完整实操教程.md
    extracted: 0.80
    inferred: 0.20
summary: obsidian-wiki 通过 .manifest.json 记录每个 source 的路径、时间戳和内容哈希，实现增量 ingest——只处理新增或修改过的文件，避免重复花费 token。
created: 2026-05-21
updated: 2026-05-21
base_confidence: 0.67
lifecycle: draft
lifecycle_changed: 2026-05-21
tier: supporting
provenance:
  extracted: 0.80
  inferred: 0.20
  ambiguous: 0.00
relationships:
  - target: "[[entities/obsidian-wiki]]"
    type: derived_from
  - target: "[[concepts/knowledge-distillation-pipeline]]"
    type: related_to
---

# Wiki Delta Tracking

Delta Tracking 是 obsidian-wiki 最被低估的设计。`.manifest.json` 记录每个 source 的路径、时间戳、对应生成的 wiki 页面和内容哈希，下次跑 `/wiki-ingest` 时**只处理新增或修改过的文件**。

## 工作机制

### Manifest 结构

每条 source 记录包含：
- **路径**: 源文件的位置
- **时间戳**: ingest 时间、文件修改时间
- **内容哈希 (content_hash)**: SHA-256 校验，用于检测文件内容是否真正变化
- **source_type**: 文档或图片
- **pages_created / pages_updated**: 该 source 生成或更新了哪些页面

### 增量判定逻辑

1. 源路径不在 manifest 中 → 新文件，需要处理
2. 源路径在 manifest 中，但 content_hash 不同 → 文件被修改，需要重新处理
3. 源路径在 manifest 中，content_hash 匹配 → **跳过**，即使修改时间不同（可能是 git checkout、文件复制等导致的 mtime 变化）^[extracted]

### 为什么用哈希而不是 mtime

时间戳不可靠——git checkout、NFS 时间戳漂移、文件复制都可能导致 mtime 变化但内容未变。content_hash 是真正的内容校验，确保只在内容确实变化时才重新处理。^[inferred]

## 成本控制意义

这种"只处理 delta"的模式让长期使用的成本几乎线性增长，不会随 vault 增大而爆炸。^[extracted]

## 相关页面

- [[entities/obsidian-wiki]] — 使用此机制的完整工具
- [[concepts/knowledge-distillation-pipeline]] — 蒸馏管线整体流程
- [[concepts/provenance-tracking]] — 来源追踪机制
