---
title: obsidian-wiki
category: entities
tags: [obsidian-wiki, knowledge-management, AI-tools, obsidian]
sources:
  - path: _raw/obsidian-wiki-完整实操教程.md
    extracted: 0.75
    inferred: 0.25
summary: obsidian-wiki 是一组让 AI 编程代理自动维护 Obsidian 知识库的 Markdown skill 文件集合，实现 Karpathy LLM Wiki 模式的完整工程化落地。
created: 2026-05-21
updated: 2026-05-21
base_confidence: 0.67
lifecycle: draft
lifecycle_changed: 2026-05-21
tier: supporting
provenance:
  extracted: 0.75
  inferred: 0.25
  ambiguous: 0.00
relationships:
  - target: "[[concepts/knowledge-distillation-pipeline]]"
    type: uses
  - target: "[[concepts/wiki-delta-tracking]]"
    type: uses
  - target: "[[concepts/provenance-tracking]]"
    type: uses
  - target: "[[concepts/karpathy-llm-wiki-pattern]]"
    type: implements
  - target: "[[concepts/context-engineering]]"
    type: related_to
---

# obsidian-wiki

obsidian-wiki（GitHub 1.1k★，MIT，v2026.05）是一组让任意 AI 编程代理读懂并执行的 Markdown skill 文件，配合 Obsidian 作为"viewer"，把"读资料 → 抽概念 → 写 wiki 页"的全流程交给 LLM。

它不是 Obsidian 插件，也不是独立 CLI，而是一套 **skill 定义文件**，通过 symlink 分发到各代理的 skills 目录。

## 核心架构

```
obsidian-wiki/
├── .skills/                    ← 所有能力的"权威定义"
│   ├── wiki-setup/SKILL.md     ← 教 LLM 怎么初始化 vault
│   ├── wiki-ingest/SKILL.md    ← 教 LLM 怎么蒸馏文档
│   ├── wiki-query/SKILL.md     ← 教 LLM 怎么从 wiki 找答案
│   └── ... 13+ 个 skill
├── CLAUDE.md / GEMINI.md / AGENTS.md
├── .cursor/rules/   .windsurf/rules/   .kiro/steering/
└── setup.sh
```

## 支持的代理

Claude Code、Cursor、Windsurf、Gemini CLI、Codex、GitHub Copilot（VS Code & CLI）、Aider、Hermes、OpenClaw、OpenCode、Factory Droid、Trae、Kiro。^[extracted]

## 安装方式

- **npx 方式**: `npx skills add Ar9av/obsidian-wiki`
- **git clone**: `git clone https://github.com/Ar9av/obsidian-wiki.git && bash setup.sh`

## 核心斜杠命令

| 命令 | 功能 |
|---|---|
| `/wiki-setup` | 初始化 vault 结构 |
| `/wiki-ingest` | 蒸馏文档为知识页面 |
| `/wiki-query` | 自然语言查询 vault |
| `/wiki-update` | 同步当前项目知识进 vault |
| `/wiki-history-ingest` | 蒸馏历史对话 |
| `/wiki-research` | 自主联网研究 |
| `/wiki-lint` | 检查断链、孤立页 |
| `/wiki-status` | 总览摄入进度 |
| `/cross-linker` | 补全缺失 wikilinks |
| `/tag-taxonomy` | 统一 tag 词汇 |
| `/graph-colorize` | 知识图谱上色 |
| `/wiki-export` | 导出知识图谱 |

## 设计哲学

obsidian-wiki 的核心洞察是：**知识编译一次，然后让 LLM 帮你维护**。它不替代 Notion/Obsidian，而是替代你"以后整理"的拖延——蒸馏权交给 LLM，你只管扔原料。^[inferred]

## 参考

1. 项目仓库：Ar9av/obsidian-wiki
2. [保姆级教程](https://jishuzhan.net/article/2053494855830142978)

## 相关页面

- [[concepts/knowledge-distillation-pipeline]] — 四阶段蒸馏管线
- [[concepts/wiki-delta-tracking]] — 增量处理机制
- [[concepts/provenance-tracking]] — 来源追踪标记
- [[concepts/karpathy-llm-wiki-pattern]] — Karpathy 原始模式
- [[concepts/context-engineering]] — Context 工程框架
- [[synthesis/obsidian-wiki-workflow]] — 日常工作流
