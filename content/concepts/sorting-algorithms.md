---
title: 排序算法
category: concepts
tags: [algorithm, Java, sorting]
sources: ["F:/blog/my-blog/blogs/algorithm/paixu.md"]
summary: 经典排序算法总结：冒泡、选择、插入（O(n²)）、希尔、归并、快速（O(n log n)）、计数、基数、桶排序，含 Java 实现与复杂度分析。
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

# 排序算法

## 比较类排序

| 算法 | 平均时间 | 最好 | 最坏 | 空间 | 稳定性 |
|---|---|---|---|---|---|
| 冒泡排序 | O(n²) | O(n) | O(n²) | O(1) | 稳定 |
| 选择排序 | O(n²) | O(n²) | O(n²) | O(1) | 不稳定 |
| 插入排序 | O(n²) | O(n) | O(n²) | O(1) | 稳定 |
| 希尔排序 | O(n log n) | O(n) | O(n²) | O(1) | 不稳定 |
| 归并排序 | O(n log n) | O(n log n) | O(n log n) | O(n) | 稳定 |
| 快速排序 | O(n log n) | O(n log n) | O(n²) | O(log n) | 不稳定 |
| 堆排序 | O(n log n) | O(n log n) | O(n log n) | O(1) | 不稳定 |

## 非比较类排序

| 算法 | 时间 | 空间 | 适用场景 |
|---|---|---|---|
| 计数排序 | O(n+k) | O(k) | 整数、范围小 |
| 桶排序 | O(n+k) | O(n+k) | 均匀分布 |
| 基数排序 | O(n×k) | O(n+k) | 整数、位数固定 |

> 基于比较的排序算法时间复杂度下界为 O(n log n) ^[inferred]

## 相关页面
- [[concepts/greedy-algorithm]]
- [[concepts/stack-and-heap]] — 堆排序依赖堆数据结构
