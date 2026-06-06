---
type: meta
title: "知识库仪表盘"
updated: 2026-06-06
---
# 知识库仪表盘

## 最近活动

```dataview
TABLE type AS 类型, status AS 状态, updated AS 更新日期
FROM "wiki"
SORT updated DESC
LIMIT 15
```

## 种子页面（待发展）

```dataview
LIST
FROM "wiki"
WHERE status = "seed"
SORT updated ASC
```

## 各领域页面数量

```dataview
TABLE length(rows) AS 页面数
FROM "wiki"
FLATTEN tags AS t
WHERE contains(t, "领域/")
GROUP BY t
```

## 缺少来源的概念

```dataview
LIST
FROM "wiki/concepts"
WHERE !sources OR length(sources) = 0
```

## 已读书籍

```dataview
TABLE author AS 作者, rating AS 评分
FROM "wiki/sources"
WHERE source_type = "book" AND status = "finished"
SORT author ASC
```

## 待读书籍

```dataview
TABLE author AS 作者
FROM "wiki/sources"
WHERE source_type = "book" AND status = "to-read"
SORT author ASC
```

## 统计概览

| 指标 | 数量 |
|------|------|
| 已读书籍 | ~40 |
| 待读书籍 | ~20+ |
| 知识卡片（待迁移） | ~70+ |
| Wiki 页面总数 | 初始化中 |
| 领域页面 | 7 |
