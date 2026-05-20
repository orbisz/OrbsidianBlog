---
title: 贪心算法
category: concepts
tags: [algorithm, Java]
sources: ["F:/blog/my-blog/blogs/algorithm/tanxin.md"]
summary: 贪心算法在每一步选择中都采取当前状态下的最优解，期望通过局部最优达到全局最优。涵盖经典问题及与动态规划的对比。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.60
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.65
  inferred: 0.25
  ambiguous: 0.10
---

# 贪心算法 (Greedy Algorithm)

贪心算法的核心策略：在每一步都选择当前状态下的最优解（局部最优），期望通过一系列局部最优选择达到全局最优解。

## 适用条件

贪心算法不一定能获得全局最优解，需要满足以下条件之一：
- **贪心选择性质**: 全局最优可以通过局部最优获得
- **最优子结构**: 问题的最优解包含子问题的最优解

## 经典应用

- **Prim 算法**: 最小生成树，每次选最小权值边
- **Kruskal 算法**: 最小生成树，每次选不形成环的最小边
- **Dijkstra 算法**: 单源最短路径
- **Huffman 编码**: 数据压缩的最优前缀编码
- **区间调度**: 选择最多不重叠区间

## 相关页面
- [[concepts/graph-data-structure]] — Prim/Kruskal/Dijkstra 均为贪心算法
- [[concepts/union-find]]
- [[concepts/sorting-algorithms]]
