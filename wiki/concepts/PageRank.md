---
type: concept
title: "PageRank"
complexity: basic
domain:
  - 科学
aliases: []
created: 2026-06-06
updated: 2026-06-06
tags:
  - 类型/概念
  - 领域/科学
status: seed
related:
sources:
  - "[[wiki/sources/数学之美]]"
---

# PageRank

## 定义
Google创始人拉里·佩奇和谢尔盖·布林发明的网页质量排名算法，通过链接关系评估网页重要性。

## 核心解释
PageRank的核心思想是：在互联网中，一个网页被越多高质量的网页链接，它本身就越重要。这就像学术论文的引用机制——被大量引用的论文通常更有影响力。PageRank不仅计算链接数量，还考虑链接来源的质量，形成了一个优雅的迭代计算体系。

PageRank的巧妙之处在于它将网页排序问题转化为一个数学问题——求解一个巨大矩阵的特征向量。这个算法是Google早期成功的核心技术，也是数学之美在实际应用中的经典案例。它证明了：在信息爆炸的时代，关键不是找到信息，而是有效地排序和筛选信息。

## 相关概念
- [[TF-IDF]]
- [[信息熵]]
