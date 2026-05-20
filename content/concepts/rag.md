---
title: RAG (Retrieval-Augmented Generation)
category: concepts
tags: [AI, RAG, LLM, vector-database]
sources: ["F:/blog/my-blog/blogs/AI/RAG.md"]
summary: RAG (检索增强生成) 通过将外部知识库与LLM结合，实现基于私有文档的精准问答。涵盖工作流程、分块策略、向量化技术、高级RAG变体及优化方法。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.70
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.75
  inferred: 0.20
  ambiguous: 0.05
---

# RAG (Retrieval-Augmented Generation)

RAG 将信息检索与LLM文本生成相结合，让模型在生成回答前先从外部知识库检索相关上下文，提升回答的事实准确性和时效性。

## RAG 工作流程

RAG 分为两个阶段：

### 文档预处理与向量库构建
- **非结构化加载器**: 适配不同文件格式（.docx/.xlsx/.pdf），提取文本内容为纯文本流
- **数据切片**: 基于语义与长度约束对文本分段切割，生成语义完整的文本块（Chunks）
- **向量化 (Embedding)**: 用预训练模型将文本块转化为高维向量，语义相似的文本在向量空间中距离更近
- **向量数据库**: 存储向量并构建索引，支持基于余弦相似度的快速语义检索

### 问答推理阶段
- 用户问题向量化 → 向量相似度检索 → 召回相关段落 → 拼入 Prompt 模板 → LLM 生成回答

## 数据分块策略

- **固定长度切分**: 按字符数/token 数硬性划分，实现简单但可能切断语义 ^[inferred]
- **滑动窗口切分**: 设置重叠区域缓解语义断裂，但增加数据冗余
- **语义切分**: 依据标点、段落结构等语义标识划分，保留文本完整性
- **父子分段模式**: 父区块保留丰富上下文，子区块实现精准匹配；问答准确率提升 30% ^[inferred]

## RAG 架构分类

- **Naive RAG**: 基础实现，简单问答场景
- **Advanced RAG**: 检索前后增加处理（查询重写、Re-ranking、上下文压缩）
- **Modular RAG**: 可互换模块（Search、Memory、Routing），支持复杂定制流程
  - Agentic RAG: 智能体驱动，循环迭代、动态决策、多工具调用

## 高级 RAG 优化方法

### 索引与检索
- **HNSW**: 多层图结构的近似最近邻搜索算法
- **MSTG**: 多尺度树图向量索引，结合树算法和图算法优势
- **混合检索**: 向量检索 + BM25 关键词检索互补

### 查询优化
- **查询重写**: 模糊/口语化查询改写为精确表述
- **回退提示 (Step-back)**: 先生成背景问题再结合原问题检索
- **子查询分解**: 复杂查询拆为多个简单子查询

### 后检索优化
- **重排序 (Re-ranking)**: 两阶段流程（粗排召回 + 精排筛选），Cross-Encoder 深度交互评分
- **上下文压缩**: 过滤无关内容，节省 token 并降低幻觉
- **上下文增强检索**: 检索时带上相邻块避免孤岛片段

### 前沿方法
- **Self-RAG**: LLM 自判断是否需要检索及检索内容，六个反思/决策点
- **CRAG**: 检索后评估相关度，低相关则切换网络搜索
- **Graph RAG**: 基于知识图谱的实体关系扩展检索
- **HyDE**: 用 LLM 生成假设文档嵌入替代 query 嵌入检索
- **多模态 RAG**: 文本 + 图像联合检索

## 传统 RAG vs Agentic RAG

| 维度 | 传统 RAG | Agentic RAG |
|---|---|---|
| LLM 定位 | 被动内容生成器 | 主动智能决策者 |
| 流程结构 | 线性单向 | 循环迭代，多决策节点 |
| 工具支持 | 仅向量数据库 | 多类型工具（搜索、API、SQL等） |
| 自我评估 | 无 | 具备自我评估和修正能力 |

## 参考文档
1. [RAG优化字典：20种RAG优化方法全解析](https://mp.weixin.qq.com/s/HR-Y1IEbHix_N3m0VBo9IQ)

## 相关页面
- [[concepts/context-engineering]] — RAG 是 Context Engineering 的基石
- [[concepts/mcp-model-context-protocol]] — Agent 工具调用协议
- [[concepts/agent-context-memory]] — Agent 上下文记忆管理
- [[concepts/transformer]] — Transformer 中的 Attention 机制
