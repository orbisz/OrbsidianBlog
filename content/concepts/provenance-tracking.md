---
title: Provenance Tracking（来源追踪）
category: concepts
tags: [knowledge-management, AI, provenance, obsidian-wiki]
sources:
  - path: _raw/obsidian-wiki-完整实操教程.md
    extracted: 0.85
    inferred: 0.15
summary: obsidian-wiki 的来源追踪机制，将每条知识声明标记为 extracted（直接抽取）、inferred（推断）或 ambiguous（存疑），写入 frontmatter 的 provenance 比例，让用户区分 AI 编了多少。
created: 2026-05-21
updated: 2026-05-21
base_confidence: 0.67
lifecycle: draft
lifecycle_changed: 2026-05-21
tier: supporting
provenance:
  extracted: 0.85
  inferred: 0.15
  ambiguous: 0.00
relationships:
  - target: "[[entities/obsidian-wiki]]"
    type: derived_from
  - target: "[[concepts/knowledge-distillation-pipeline]]"
    type: related_to
---

# Provenance Tracking（来源追踪）

每条声明都会被打上三类来源标签写入 frontmatter，可追溯性比一般"用 AI 总结"高了一个量级。^[extracted]

## 三类来源标签

| 标签 | 含义 | 标记方式 |
|---|---|---|
| **extracted** | 源材料明确陈述的内容 | 无需标记（默认） |
| **inferred** | LLM 基于语义推断的内容 | 行尾加 `^[inferred]` |
| **ambiguous** | 源材料有分歧或表述模糊 | 行尾加 `^[ambiguous]` |

## Frontmatter 比例

每个页面的 frontmatter 会记录大致比例：

```yaml
provenance:
  extracted: 0.7
  inferred: 0.3
  ambiguous: 0.0
```

例如 `extracted: 0.7 / inferred: 0.3` 意味着该页 70% 来自原文直接抽取，30% 是 LLM 推断。出现冲突时你知道该重点核对哪部分。^[extracted]

## 杀手特性

这是 obsidian-wiki 的核心差异化设计——它强制你直面"AI 编了多少"。一般 AI 摘要工具不会告诉你哪些是忠实原文、哪些是 AI 发挥的。^[inferred]

## 多模态场景

图像源由于视觉解读的天然不确定性，衍生页面会倾向于高 `inferred` 比例。provenance 标记的存在正是为了显式标记这种不确定性。^[inferred]

## 相关页面

- [[entities/obsidian-wiki]] — 使用此机制的完整工具
- [[concepts/knowledge-distillation-pipeline]] — 蒸馏管线中应用 provenance 的阶段
- [[concepts/wiki-delta-tracking]] — 增量处理机制
