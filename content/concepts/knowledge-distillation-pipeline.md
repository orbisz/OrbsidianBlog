---
title: Knowledge Distillation Pipeline
category: concepts
tags: [knowledge-management, AI, pipeline, obsidian-wiki]
sources:
  - path: _raw/obsidian-wiki-完整实操教程.md
    extracted: 0.80
    inferred: 0.20
summary: obsidian-wiki 的四阶段知识蒸馏管线：Ingest（读取源材料）→ Extract（抽概念/实体/关系）→ Resolve（合并或新建页面）→ Schema（维护一致性和 wikilinks）。
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
  - target: "[[concepts/provenance-tracking]]"
    type: uses
  - target: "[[concepts/wiki-delta-tracking]]"
    type: related_to
---

# Knowledge Distillation Pipeline

obsidian-wiki 的核心工作原理是一个四阶段管线，将源材料蒸馏为结构化的知识页面：

```
源材料 (markdown / PDF / JSONL / 截图)
   │
   ▼
[1] Ingest  ── 直接读取，不做预处理
   │
   ▼
[2] Extract ── 抽概念、实体、关系、open questions
   │
   ▼
[3] Resolve ── 与现有 wiki 合并 / 新建页面
   │
   ▼
[4] Schema  ── 维护 schema 一致性、补 wikilinks
   │
   ▼
   生成 wiki 页面 + 更新 .manifest.json
```

## 四个阶段详解

### Stage 1: Ingest

直接读取源材料，不做预处理。支持的格式包括 markdown、PDF、JSONL、截图等。^[extracted]

### Stage 2: Extract

从源材料中抽取：
- **Key concepts** — 值得独立成页的概念
- **Entities** — 人物、工具、项目、组织
- **Claims** — 可归因于源材料的声明
- **Relationships** — 概念间关系及类型
- **Open questions** — 源材料提出但未回答的问题

### Stage 3: Resolve

与现有 wiki 页面比对，决定是合并到已有页面还是创建新页面。这是增量更新的关键——不会重复创建已有内容。^[inferred]

### Stage 4: Schema

维护页面分类和 frontmatter 字段的一致性，补全 wikilinks，确保知识图谱连通性。

## 与一般"AI 总结"的区别

这个管线不是简单的文本摘要，而是**结构化知识蒸馏**：
1. 抽取的内容被打上来源标签（extracted / inferred / ambiguous）
2. 结果是相互链接的结构化页面，而非一段文本
3. 支持增量处理，只处理新增/修改过的源材料

## 相关页面

- [[entities/obsidian-wiki]] — 使用此管线的工具
- [[concepts/provenance-tracking]] — 来源追踪机制
- [[concepts/wiki-delta-tracking]] — 增量处理机制
- [[concepts/karpathy-llm-wiki-pattern]] — 原始设计理念
