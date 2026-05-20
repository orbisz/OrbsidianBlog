---
title: Agent 上下文记忆管理
category: concepts
tags: [AI, AI-Agent, memory, context]
sources: ["F:/blog/my-blog/blogs/AI/Memory.md"]
summary: Agent 长对话场景下的智能上下文管理方案，通过自动压缩、卸载和摘要对话历史，在成本控制和信息保留之间寻找平衡。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.65
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.60
  inferred: 0.30
  ambiguous: 0.10
---

# Agent 上下文记忆管理

长对话场景中，Agent 面临的核心挑战：
- **成本线性增长**: 每次 API 调用为所有历史 tokens 付费
- **性能下降**: 上下文越长，处理越慢
- **maxToken 限制**: 超出上下文窗口则请求失败
- **信息丢失**: 简单截断丢失关键历史信息

## AutoContextMemory 架构

AgentScope 的智能上下文内存管理组件，采用多存储架构：

### 四层存储
- **工作内存 (Working Memory)**: 压缩后的消息，直接参与推理
- **原始内存 (Original Memory)**: 完整未压缩历史，仅追加模式
- **卸载上下文存储**: UUID 为键存储卸载内容，按需重载
- **压缩事件存储**: 记录所有压缩操作，用于分析和优化

### 六种渐进式压缩策略

压缩流程: 检查阈值 → 策略1 → 策略2 → 策略3 → 策略4 → 策略5 → 策略6

1. **压缩历史工具调用**: 查找连续工具调用（>6条），LLM 智能压缩保留关键信息
2. **卸载大型消息（带保护）**: 卸载超过阈值的大型消息，保护最新助手响应和最后 N 条消息
3. **卸载大型消息（无保护）**: 更激进的卸载，仅保护最新助手响应
4. **摘要历史对话轮次**: LLM 对历史用户-助手对话对进行智能摘要
5. **摘要当前轮次大型消息**: 针对当前轮次超阈值消息生成摘要
6. **压缩当前轮次消息**: 最后的保障策略，合并工具结果保留关键信息

### 压缩原则
- **当前轮次优先**: 优先保护当前轮次完整信息
- **用户交互优先**: 用户输入和 Agent 回复的重要性 > 工具调用中间结果
- **可回溯性**: 所有压缩原文可通过 UUID 回溯

## 参考
1. [AgentScope AutoContextMemory](https://mp.weixin.qq.com/s/SGGJWfhlYtUUieO_hl45jw)

## 相关页面
- [[concepts/context-engineering]] — Context 工程的整体框架
- [[concepts/rag]] — RAG 的知识检索
