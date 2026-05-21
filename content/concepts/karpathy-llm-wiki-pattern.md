---
title: Karpathy's LLM Wiki Pattern
category: concepts
tags: [knowledge-management, LLM, AI-workflow, obsidian-wiki]
sources:
  - path: _raw/obsidian-wiki-完整实操教程.md
    extracted: 0.70
    inferred: 0.30
summary: Andrej Karpathy 提出的知识管理模式：将知识编译一次为互联的 markdown 文件，然后让 LLM 持续维护。obsidian-wiki 是该模式的工程化落地。
created: 2026-05-21
updated: 2026-05-21
base_confidence: 0.60
lifecycle: draft
lifecycle_changed: 2026-05-21
tier: supporting
provenance:
  extracted: 0.70
  inferred: 0.30
  ambiguous: 0.00
relationships:
  - target: "[[entities/obsidian-wiki]]"
    type: derived_from
  - target: "[[concepts/knowledge-distillation-pipeline]]"
    type: related_to
  - target: "[[concepts/context-engineering]]"
    type: related_to
---

# Karpathy's LLM Wiki Pattern

Andrej Karpathy 在其经典的 LLM Wiki gist 中给出了一个朴素但强大的方案：

> Compile knowledge **once** into interconnected markdown files, then let the LLM keep them current.

把知识编译一次，然后让 LLM 帮你维护。^[extracted]

## 核心思想

1. **编译一次**: 人工或 AI 将非结构化知识（对话、文档、经验）转化为结构化的 markdown 页面
2. **互联**: 页面之间通过 wikilinks 建立关联，形成知识图谱
3. **LLM 维护**: 后续的更新、合并、补充由 LLM 自动完成，而非人工整理

## 解决的痛点

- 同一问题反复问 AI，每次重讲上下文
- 知识散落在对话、文档中，无法检索
- 文档"以后整理"的拖延症
- 90% 的 Obsidian 页面是 TODO^[extracted]

本质是：**知识没有被结构化沉淀，AI 也没有"持续学习你"**。^[extracted]

## 工程化实现

obsidian-wiki 是该模式的完整工程化落地：
- 通过 skill 文件教 LLM 如何执行蒸馏
- .manifest.json 实现 delta 跟踪
- provenance 标记区分 AI 推断和原文抽取
- 支持十多种 AI 编程代理^[inferred]

## 相关页面

- [[entities/obsidian-wiki]] — 该模式的工程化实现
- [[concepts/knowledge-distillation-pipeline]] — 实现该模式的核心管线
- [[concepts/context-engineering]] — Context 工程框架
- [[concepts/agent-context-memory]] — Agent 记忆管理
