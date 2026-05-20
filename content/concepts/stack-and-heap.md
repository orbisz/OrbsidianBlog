---
title: 栈与堆
category: concepts
tags: [algorithm, data-structure, Java, memory]
sources: ["F:/blog/my-blog/blogs/algorithm/stackandheap.md"]
summary: 栈（Stack）和堆（Heap）数据结构详解，包括 Java 中的内存栈/堆区别、优先队列（PriorityQueue）及堆排序原理。
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

# 栈与堆

## 数据结构层面

### 栈 (Stack)
- 后进先出 (LIFO)
- 操作: push/pop/peek
- 应用: 函数调用栈、括号匹配、DFS

### 堆 (Heap)
- 完全二叉树，父节点 >= 子节点（大顶堆）或 <=（小顶堆）
- Java: `PriorityQueue` 默认小顶堆
- 应用: Top K 问题、堆排序、Dijkstra

## JVM 内存层面

- **栈 (Stack)**: 线程私有，存储局部变量和方法调用帧
- **堆 (Heap)**: 线程共享，存储对象实例，GC 主要区域

## 相关页面
- [[concepts/sorting-algorithms]] — 堆排序
- [[concepts/graph-data-structure]] — Dijkstra 最短路径
