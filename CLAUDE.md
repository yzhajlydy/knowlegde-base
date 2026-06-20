# 个人知识库 Wiki — LLM Wiki Schema

语言：中文（界面、注释、callout 块用中文，专有名词保留原文）
模式：混合模式（Research + Personal Second Brain）
目的：系统性整理多领域交叉知识，让阅读和思考持续复利增长
创建日期：2026-06-06

---

## 架构

```
vault/
├── CLAUDE.md              ← 本文件：行为规范
├── README.md              ← 仓库门面（含概念筛选三原则）
├── raw/                   ← Layer 1: 原始素材（正文不可改）
│   ├── books/             每本书：《书名》 作者/  含 .md + image/
│   └── cards/             每张卡片：卡片名/  含 .md + image/
└── wiki/                  ← Layer 2: LLM 维护的知识库
    ├── index.md           主索引（领域入口 + 作者 + 来源；概念索引见 domains）
    ├── concepts/          概念、思想、框架（一概念一页）
    ├── sources/           每本书/课程的摘要页
    ├── authors/           作者/思想家页
    ├── domains/           领域聚合页（11个领域，每个概念一句话）
    └── meta/
        └── dashboard.md   Obsidian Dataview 动态仪表盘（自动生成）
```

> 已废弃（不再维护）：`hot.md` / `log.md` / `overview.md`。历史活动看 `git log`，运行时统计看 dashboard。

---

## 核心规则

1. **raw/ 是原始素材区。** 正文不可改；允许整理（扁平化、删空壳重复）。
2. **wiki/ 是你的。** 全权负责创建、更新、重命名、删除 wiki/ 下所有文件。
3. **每个 wiki 页面必须有 YAML frontmatter。** 无例外。
4. **使用 Wikilinks。** `[[页面名]]` 而非 `[text](path/to/file.md)`。文件名必须唯一。
5. **原子化笔记。** 一个概念一个页面。
6. **更新而非重复。** 概念已有页面就更新，不新建。
7. **中文为主。** 人名/专有名词保留原文或中英对照。
8. **双向链接。** A 链接 B 时，检查 B 是否也应链接回 A。
9. **保持页面精简。** 每页 100-300 行。

---

## 概念筛选（入选门槛）

新概念入选前必须跑三问（详见 [[概念筛选三原则]]）：**反直觉、可迁移、可运算**。三项全过才建页面，否则不纳入。这是知识库的元规则，优先于一切"多记一点"的冲动。

---

## Frontmatter 规范

### 通用字段（每个页面必须有）：
```yaml
---
type: source|concept|entity|domain|meta
title: "人类可读标题"
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags:
  - 标签1
status: seed|developing|mature|archived
related:
  - "[[其他页面]]"
sources:
  - "[[raw/books/某本书笔记.md]]"
---
```

### 类型特有字段：

**source 类型**（书/课程摘要）：
```yaml
source_type: book|course|article|podcast
author: "作者名"
status: reading|finished|to-read
rating: 1-5（可选）
key_takeaways:
  - "要点1"
```

**concept 类型**（概念/思想）：
```yaml
complexity: basic|intermediate|advanced
domain:
  - 经济学
aliases:
  - 别名1
```

**entity 类型**（作者/人物，存放于 `wiki/authors/`）：
```yaml
entity_type: person
role: "角色描述"
field: "领域"
```

---

## 三种操作

### INGEST（摄入）

触发：用户将文件放入 raw/ 或粘贴内容。

流程：
1. 完整阅读素材。
2. 与用户讨论关键收获（用户说"直接摄入"时跳过）。
3. **对每个候选概念跑筛选三问**——不达标的不建页面。
4. 在 `wiki/sources/` 创建素材摘要页。
5. 为每个重要作者创建或更新 `wiki/authors/` 页面。
6. 为每个达标概念创建或更新 `wiki/concepts/` 页面。
7. 更新相关的 `wiki/domains/` 领域页。
8. 发现矛盾时在两个页面用 callout 标记：`> [!矛盾] [[页面A]] 声称 X，但 [[页面B]] 认为是 Y。`

> 不再维护 hot/log/overview。index.md 只在来源/作者有变化时更新；概念索引交给 domains/。

### QUERY（查询）

触发：用户提出任何问题。

流程：
1. 读 `wiki/index.md` 定位相关领域/来源。
2. 读对应 `wiki/domains/` 领域页定位概念。
3. 读 3-5 个相关 `wiki/concepts/` 页面（超过 10 个说明定位不精）。
4. 综合回答，用 wikilinks 引用来源。
5. 提供"将此回答保存为 wiki 页面"的选项（先过筛选三问）。
6. 暴露知识缺口时主动提出"关于 X 我了解不足，是否需要查找素材？"

### LINT（检查）

触发：用户说"检查 wiki"或每 15-20 次摄入后。

检查项目：孤立页面、死链接、过时信息、缺失页面、缺失交叉引用、Frontmatter 缺失/不完整、空章节、未解决的 `[!矛盾]` 标记。

输出：`wiki/meta/lint-report-YYYY-MM-DD.md`。不要自动修复，先征求用户同意。

---

## 写作风格

- 陈述式，现在时。"X 采用 Y 方法"而不是"X 基本上是 Y"。
- 大量使用 wikilinks。每次提及已有概念都加链接。
- 引用来源：`(来源: [[页面]])`
- callout 标记：`[!待验证]` `[!矛盾]` `[!关键洞察]` `[!缺口]`

---

## 上下文窗口管理

- 先读 `wiki/index.md`（领域入口 + 来源），再读对应 `domains/` 领域页
- 每次查询只读 3-5 个完整概念页
- 用搜索做关键词定位，不要全文扫描
- 用 Edit 做精确编辑，不要重写整个文件来改一个字段
- 不要把 wiki 内容粘贴到对话中，除非用户要求。用 wikilink 引用。

---

## 领域标签体系

- `#领域/经济学` `#领域/心理学` `#领域/管理学` `#领域/认知科学` `#领域/哲学` `#领域/科学` `#领域/思维方法` `#领域/自我提升` `#领域/商业` `#领域/历史` `#领域/科技`
- `#类型/概念` `#类型/人物` `#类型/书籍` `#类型/课程`
- `#状态/种子` `#状态/发展中` `#状态/成熟` `#状态/待读`

---

## 文件命名规范

- **文件名**：中文，可带空格（`损失规避.md`）
- **目录名**：小写英文（`wiki/concepts/`）
- **标签**：中文，层级用斜杠（`#领域/经济学`）
- **文件名唯一**：确保 wikilinks 无需路径即可工作
