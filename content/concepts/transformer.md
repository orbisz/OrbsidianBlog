---
title: Transformer 架构
category: concepts
tags: [AI, Transformer, deep-learning, NLP]
sources: ["F:/blog/my-blog/blogs/AI/transformer.md"]
summary: Transformer 是第一个完全依赖自注意力机制（Self-Attention）的序列转换模型，涵盖 BPE 分词、位置编码（PE）、多头注意力、编码器-解码器结构及 PyTorch 实现。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.75
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.80
  inferred: 0.15
  ambiguous: 0.05
---

# Transformer 架构

Transformer 是第一个完全依赖自注意力（Self-Attention）来计算输入和输出表示，而不使用 RNN 或 CNN 的序列转换模型。

## 输入编码: BPE + PE

### BPE 分词 (Byte Pair Encoding)

BPE 是一种子词（Subword）分词算法，核心逻辑是从最小字符单元开始，反复合-并高频字节对，直到达到预设词表大小。

**BPE 的核心价值**: 通过子词平衡词汇量和语义颗粒度的矛盾——既能控制词汇量，又能处理 OOV（Out-of-Vocabulary），同时保留一定语义粒度。^[inferred]

**算法步骤**:
1. 准备训练语料，确定 subword 词表大小
2. 将单词拆分为字符序列，末尾加后缀
3. 统计连续字节对出现频率，合并最高频对
4. 重复直到达到词表大小或最高频对频率为 1
5. 新词按最长匹配原则拆分为已有子词

### 位置编码 (Positional Encoding)

Transformer 并行处理所有 token，天然无法捕捉序列位置关系。PE 通过数学方式给每个 token 的嵌入向量附加位置信息。

PE 的四个核心设计原则：
1. 与嵌入向量兼容（维度一致）
2. 支持任意序列长度
3. 捕捉相对位置关系
4. 计算高效

经典实现使用正弦/余弦函数，第 pos 个位置第 i 维：
- 偶数维: `PE(pos, 2i) = sin(pos / 10000^(2i/d_model))`
- 奇数维: `PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))`

**常见的 PE 变体**:

| 类型 | 核心思路 | 典型应用 |
|---|---|---|
| 可学习 PE (Learned PE) | 随机初始化 PE 矩阵，通过训练学习 | BERT, T5 |
| 旋转位置编码 (RoPE) | 将位置信息编码为旋转矩阵 | LLaMA, ChatGLM, Qwen |
| 相对位置编码 | 在注意力计算时直接建模相对距离 | Transformer-XL, DeBERTa |
| ALiBi | 不给 token 注入 PE，而是在注意力权重上附加线性衰减偏置 | PaLM |

## 网络结构

### 多头自注意力 (Multi-Head Self-Attention)

Self-Attention 的核心：通过 Q（Query）、K（Key）、V（Value）计算注意力权重。

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V$$

- **缩放因子** `1/√d_k`: 防止点积方差随维度增长，使 softmax 分布与维度解耦，保持训练梯度稳定
- **多头机制**: 将 Q、K、V 拆分为多个子空间分别计算 Self-Attention，类似 CNN 的多通道机制，让模型同时关注多个不同信息

> 注意：MultiHead 的 head 数不影响参数量——输入维度固定时，拆成多少头参数都一样

### 前馈层 (Feed Forward)
两层全连接网络 + ReLU 激活，隐状态维度通常大于自注意力子层。

### 残差连接与层归一化
通过直连通道将子层输入连接到输出，缓解深层优化中的梯度消失问题。

### 编码器-解码器
- **编码器**: 自注意力 + 前馈，融合源语言序列的上下文语义
- **解码器**: 掩码自注意力（防止看到未来信息）+ 交叉注意力（接收编码器输出），自回归生成目标序列

## 参考文献
1. [万字长文说明白transformer](https://zhuanlan.zhihu.com/p/657456977)
2. [如何训练你的BERT](https://zhuanlan.zhihu.com/p/163511181)
3. [transformer结构-输入编码(BPE,PE)剖析](https://zhuanlan.zhihu.com/p/667635031)

## 相关页面
- [[concepts/rag]] — RAG 系统中使用 Transformer 架构
- [[concepts/context-engineering]] — Prompt/Context 工程与 LLM 的交互
