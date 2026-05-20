---
title: Context Engineering
category: concepts
tags: [AI, Prompt-Engineering, LLM, RAG]
sources: ["F:/blog/my-blog/blogs/AI/Prompt.md"]
summary: Context Engineering 是设计和优化动态自动化系统的学科，在正确的时间为 LLM 提供正确的信息和工具。Prompt Engineering 是其子集，RAG 是其核心架构模式。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.70
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.60
  inferred: 0.30
  ambiguous: 0.10
---

# Context Engineering

Context Engineering 是一门设计、构建并优化动态自动化系统的学科，旨在为 LLM 在正确的时间、以正确的格式，提供正确的信息和工具。

> Prompt 告诉模型**如何思考**，而 Context 赋予模型完成工作所需的**知识和工具**。

## Prompt Engineering 基础

### Prompt 设计六要素
```
Prompt = 角色(Role) + 上下文(Context) + SOP(Workflow) + 边界(Boundary) + 回答约束(Constraints) + 示例(Examples)
```

### 核心提示技术
- **零样本提示 (Zero-Shot)**: 不提供示例，依赖模型预训练知识
- **少样本提示 (Few-Shot)**: 提供 1-5 个高质量示例引导模型行为
- **思维链 (CoT)**: 引导模型将复杂问题分解为中间推理步骤
- **ReAct**: 思考-行动-观察循环，将问题分解为具体行动步骤

### Prompt Engineering 的局限性
- **脆弱性**: 微小措辞变化可能导致输出巨大差异 ^[inferred]
- **扩展性差**: 手动迭代优化难以规模化
- **无状态性**: 本质上是单轮交互设计

## Context Engineering vs Prompt Engineering

| 维度 | Prompt Engineering | Context Engineering |
|---|---|---|
| 范围 | 上下文窗口内的具体指令 | 整个信息生态系统的设计 |
| 焦点 | 单个提示的优化 | 系统级自动化 |
| 关系 | 是 Context Engineering 的子集 | 包含 Prompt Engineering |

## Context 的信息生态

LLM 在做出响应前能看到的全部信息包括：
- 系统级指令和角色设定
- 对话历史（短期记忆）
- 持久化用户偏好（长期记忆）
- 动态检索的外部数据（RAG）
- 可用工具及定义
- 期望的输出格式

## Lost in the Middle

LLM 在处理长上下文时表现出 U 型性能曲线：关键信息在开头（首因效应）或结尾（近因效应）时模型表现好，但信息在中间时性能显著下降。

> 问题不在于模型"找不到"信息，而在于信息检索和信息利用之间存在脱节 ^[ambiguous]

## 上下文窗口优化策略

### LangChain 四策略
1. **Write (持久化)**: Scratchpads（会话内临时记忆）+ Memory（跨会话长期存储）
2. **Select (检索)**: 动态 RAG 选择相关上下文，包括对工具描述的 RAG
3. **Compress (压缩)**: 摘要/修剪管理不断增长的上下文
4. **Isolate (隔离)**: 多智能体系统拆分上下文，沙盒环境隔离工具调用

## 智能体编排架构

### 工作流 vs 智能体
- **工作流**: 预定义代码路径编排，确定性高，适合明确业务流程
- **智能体**: LLM 动态指导流程和工具使用，灵活性高

### 核心编排模式
- **链式工作流 (Prompt Chaining)**: 模块 A → 模块 B → 最终输出
- **路由工作流 (Routing)**: 路由器分析输入 → 选择业务模块
- **编排器-工作者 (Orchestrator-Workers)**: 中心智能体分解任务 → 专职工作者执行

### ReAct 框架
循环: 思考(Thought) → 行动(Action) → 观察(Observation) → 再思考。数据流根据 LLM 的推理结果动态生成。

### Reflection 机制
评估器模块反馈循环：执行结果 → 评估（成功/失败/信息不足）→ 调整规划路径。

## 参考
1. [Context Engineering 文章](https://mp.weixin.qq.com)

## 相关页面
- [[concepts/rag]] — RAG 是 Context Engineering 的基石
- [[concepts/mcp-model-context-protocol]] — 工具集成协议
- [[concepts/agent-context-memory]] — 智能体上下文记忆管理
- [[concepts/harness-engineering]] — Harness Engineering 与 Context 的关系
