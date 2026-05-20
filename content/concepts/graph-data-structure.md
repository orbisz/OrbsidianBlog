---
title: 数据结构 — 图
category: concepts
tags: [algorithm, data-structure, Java, graph]
sources: ["F:/blog/my-blog/blogs/algorithm/graph.md"]
summary: 图的完整知识体系：基本概念（有向/无向/连通/生成树）、五种存储结构（邻接矩阵/邻接表/十字链表/邻接多重表/边集数组）、遍历（DFS/BFS）、最小生成树（Prim/Kruskal）、最短路径（Dijkstra/Floyd）、拓扑排序和关键路径。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.80
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.90
  inferred: 0.05
  ambiguous: 0.05
---

# 数据结构 — 图

图（Graph）由顶点有穷非空集合 V 和顶点之间边的集合 E 组成: G = (V, E)。

## 基本概念

- **有向图/无向图**: 边是否有方向
- **简单图**: 无自环、无多重边
- **完全图**: 无向图 n(n-1)/2 条边，有向图 n(n-1) 条弧
- **连通图**: 任意两顶点间有路径
- **强连通图/强连通分量**: 有向图中任一对顶点互相可达
- **生成树**: 包含全部顶点的极小连通子图（n-1 条边）
- **度/入度/出度**: 无向图度之和 = 2e，有向图入度之和 = 出度之和 = e

## 五种存储结构

### 邻接矩阵
二维数组存储边信息，空间复杂度 O(V²)。适合稠密图，对称矩阵可压缩存储。

### 邻接表
顶点表 + 边表，空间复杂度 O(V+E)。适合稀疏图，但确定两顶点间是否存在边效率低。

### 十字链表
有向图的链式存储。综合邻接表和逆邻接表，同时方便求出入度。

### 邻接多重表
无向图的链式存储。同一条边只有一个结点，方便删除操作。

### 边集数组
两个数组（顶点 + 边）。适合对边依次处理，不适合对顶点操作。

## 图的遍历

### DFS (深度优先)
尽可能"深"地搜索，递归实现。空间 O(V)。邻接矩阵时间 O(V²)，邻接表时间 O(V+E)。

### BFS (广度优先)
逐层访问，借助辅助队列实现。空间 O(V)。时间复杂度和 DFS 一致。

## 最小生成树 (MST)

### Prim 算法
从顶点出发，每次添加最小的边（不形成回路），时间 O(V²)。适合稠密图。

### Kruskal 算法
按边权递增排序，使用并查集判断是否成环，时间 O(E log E)。适合稀疏图。

## 最短路径

### Dijkstra 算法
单源最短路径，不能有负权值。贪心策略，时间 O(V²)。

### Floyd 算法
所有顶点对间最短路径，动态规划，时间 O(V³)。可检测负权回路。

## 拓扑排序 & 关键路径

- **AOV 网**: 顶点表示活动，拓扑排序判断工程能否顺序进行
- **AOE 网**: 边表示活动，关键路径求工程完成的最短时间
  - ve(k): 事件最早发生时间
  - vl(k): 事件最迟发生时间
  - d() = 0 的活动构成关键路径

## 参考
1. [数据结构：图(Graph)详解](https://blog.csdn.net/Real_Fool_/article/details/114141377)

## 相关页面
- [[concepts/union-find]] — Kruskal 算法依赖并查集
- [[concepts/greedy-algorithm]] — Prim/Kruskal/Dijkstra 均为贪心算法
- [[concepts/sorting-algorithms]] — Kruskal 依赖排序
