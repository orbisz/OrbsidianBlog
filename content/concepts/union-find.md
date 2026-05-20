---
title: 并查集 (Union-Find)
category: concepts
tags: [algorithm, data-structure, Java]
sources: ["F:/blog/my-blog/blogs/algorithm/union.md"]
summary: 并查集是一种树型数据结构，用于处理不相交集合的合并与查询。支持近乎 O(1) 的 Union 和 Find 操作，是 Kruskal 最小生成树算法的核心组件。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.65
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.70
  inferred: 0.20
  ambiguous: 0.10
---

# 并查集 (Union-Find)

并查集是一种树型数据结构，用于处理不相交集合（Disjoint Sets）的合并及查询问题。

## 核心操作

- **Find**: 确定元素属于哪个子集（查找代表元）
- **Union**: 将两个子集合并成一个集合

## 优化策略

- **路径压缩 (Path Compression)**: Find 时将路径上所有节点直接指向根节点
- **按秩合并 (Union by Rank)**: 将矮树合并到高树下，保持树的平衡

两种优化叠加时，均摊时间复杂度接近 O(α(n))（反阿克曼函数），近似为常数时间。

## 应用场景

- Kruskal 最小生成树算法中判断边是否形成环
- 判断图的连通分量数量
- 动态连通性问题

## 相关页面
- [[concepts/graph-data-structure]] — Kruskal 算法依赖并查集
- [[concepts/greedy-algorithm]]
- [[concepts/sorting-algorithms]]
