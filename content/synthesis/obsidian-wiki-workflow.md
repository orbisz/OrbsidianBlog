---
title: obsidian-wiki 日常工作流
category: synthesis
tags: [obsidian-wiki, workflow, knowledge-management, daily-routine]
sources:
  - path: _raw/obsidian-wiki-完整实操教程.md
    extracted: 0.75
    inferred: 0.25
summary: obsidian-wiki 推荐的日常维护节奏：每天 /wiki-update 蒸馏新知识，每周跑 history-ingest + lint + cross-linker，每月做 tag-taxonomy + graph-colorize + export，季度级 rebuild。
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
  - target: "[[entities/obsidian-wiki]]"
    type: derived_from
  - target: "[[concepts/knowledge-distillation-pipeline]]"
    type: uses
---

# obsidian-wiki 日常工作流

长期使用 obsidian-wiki 的推荐维护节奏，确保知识库持续增长且不混乱。

## 每天（5 min）

```bash
cd <today-project>
claude
> /wiki-update          # 把今天的新增蒸馏进 vault
```

`/wiki-update` 会用 `git log` 找出今天改动过的文件，提取新决策/新概念/新约定，增量写入 vault 对应分类。**不会把代码原样塞进 vault**，只蒸馏知识层面的内容。^[extracted]

## 每周（10-15 min）

```shell
> /wiki-history-ingest claude    # 这周和 Claude 聊出来的全部沉淀
> /wiki-status                   # 看看进度
> /wiki-lint                     # 找断链 / 孤立页
> /cross-linker                  # 补 wikilinks
```

历史对话是最被低估的知识来源。1.2 万条 message 约 25 分钟处理，可生成 187 个 wiki 页面，其中 `synthesis/` 里的综述最有价值。^[extracted]

## 每月（半小时）

```shell
> /tag-taxonomy           # 统一 tag（合并 #api 与 #API）
> /graph-colorize         # 重新上色（色盲友好调色板）
> /wiki-export            # 导出 graph.html，备份并分享
```

`graph.html` 是最实用的导出——双击打开浏览器即可交互浏览，分享不需要装 Obsidian。^[extracted]

## 季度

```shell
> /wiki-rebuild           # vault 实在乱了再用，会先归档再重建
```

## 关键洞察

价值密度最高的命令是 `/wiki-history-ingest`。你过去和 AI 的对话比想象中有用得多。`.manifest.json` 的 delta 模式让长期使用成本几乎线性，不会爆炸。^[inferred]

## 相关页面

- [[entities/obsidian-wiki]] — 完整工具介绍
- [[concepts/knowledge-distillation-pipeline]] — 蒸馏管线
- [[concepts/wiki-delta-tracking]] — 增量处理机制
- [[concepts/provenance-tracking]] — 来源追踪
