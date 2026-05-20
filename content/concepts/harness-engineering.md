---
title: Harness Engineering
category: concepts
tags: [AI, AI-Coding, SDD, software-engineering]
sources: ["F:/blog/my-blog/blogs/Musings/HarnessEngineering.md"]
summary: Harness Engineering 是将强大但不可控的 AI 模型嵌⼊确定性业务流水线而设计的工程控制面。核心理念：每次 Agent 犯错，工程化地消除这个错误的可能性。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.70
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.65
  inferred: 0.25
  ambiguous: 0.10
---

# Harness Engineering

Harness Engineering 的核心定义来自 Mitchell Hashimoto：

> "每当你发现 Agent 犯了一个错误，你就花时间去工程化一个解决方案，让它再也不会犯同样的错。"

## Harness 的核心隐喻

- **AI 模型 = 马**（强大但黑盒不可控）
- **Harness = 缰绳/马鞍/护具**（工程控制面）
- **骑手 = 人类工程师**（明确意图、设计环境、构建反馈回路）

## 工程纪律的转移

OpenAI 指出：纪律从「如何写好代码」转移到「如何构建支撑 Agent 工作的系统体系」——结构化的文档、明确的约束规则、完善的反馈回路。

**Agent 看不到的，就不存在。** 写进仓库的本地化版本工件才是 Agent 能看到的全部。^[inferred]

## Harness 与 Spec 的关系

Harness 和 SDD（Spec-Driven Development）不是竞争关系，而是同一件事的两个层面：
- **Harness 是放大器**，放大 Agent 的执行能力
- **Spec 是被放大的内容**，为 Agent 提供推理地图

### Spec 的三个角色
1. **Agent 推理的地图**: 给 Agent 一张地图而非 1000 页说明书，渐进式披露
2. **约束生效的语义基础**: Linter 检查格式，Spec 承载语义（接口约定、状态流转规则等）
3. **反馈回路的正确性判据**: Spec 的验收标准（WHEN/THEN Scenario）提供"正确性判据"

### 关键认知
- 人类注意力是最稀缺的资源——审查重心在 Spec，不是代码
- "大型 AGENTS.md" 是陷阱——执行约束和语义约束要分开管理
- Spec 漂移是沉默的，需要主动检测机制
- 出问题时追问方向是"AI 还缺什么"，不是"人类再努力一点"

## 参考
1. [Harness Engineering (OpenAI)](https://openai.com/zh-Hans-CN/index/harness-engineering/)
2. [Harness Engineering vs SDD](https://mp.weixin.qq.com/s/Laz4W0180y9yGW0b6EpUMQ)

## 相关页面
- [[concepts/context-engineering]] — Context 工程与 Harness 的关系
