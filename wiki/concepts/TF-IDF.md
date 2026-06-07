---
type: concept
title: "TF-IDF"
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

# TF-IDF

## 定义
词频-逆文档频率（Term Frequency-Inverse Document Frequency），一种衡量关键词与查询相关性的度量方法。

## 核心解释
TF-IDF是信息检索中最经典的方法之一。它的核心思想是：一个词对某篇文档的重要性，取决于两个方面——这个词在这篇文档中出现的频率有多高（TF），以及这个词在所有文档中出现的频率有多低（IDF）。

简单来说，如果一个词在一篇文档中反复出现（高TF），但在其他文档中很少出现（高IDF），那么这个词就是这篇文档的关键特征词。比如"量子"在一篇物理论文中频繁出现，但在整个互联网中相对罕见，那它就是很好的区分词。TF-IDF的数学之美在于它用极其简单的公式，有效地抓住了"区分度"这个信息检索的核心需求。

## 相关概念
- [[PageRank]]
- [[信息熵]]
