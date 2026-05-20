---
title: AI Coding 技术概念
category: concepts
tags: [AI, AI-Coding, developer-tools]
sources: ["F:/blog/my-blog/blogs/AI/AI_Coding_Concept.md"]
summary: AI Coding 领域核心概念梳理：Command（快捷指令）、MCP 工具调用、Agent 工作流等，涵盖 Cursor、Claude Code、Codex 等主流 AI 编程工具的技术体系。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.60
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.50
  inferred: 0.35
  ambiguous: 0.15
---

# AI Coding 技术概念

## Command

Command 是一个快捷方式，将一段预设提示词快速发送到对话中。本质上是存放在指定位置的 Markdown 文件，配置名称和描述等属性。^[inferred]

## MCP 工具

通过 MCP 协议标准化 AI 工具调用接口，实现 Agent 与外部系统的集成。

## Agent 工作流

将 AI Agent 的业务流程通过编排串联，使复杂任务可拆解为各节点逐步执行。

## 相关页面
- [[concepts/mcp-model-context-protocol]] — MCP 协议详解
- [[concepts/context-engineering]] — Context 工程与智能体
- [[concepts/harness-engineering]] — Harness 工程方法论
