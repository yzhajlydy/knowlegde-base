# 个人知识库 Wiki

基于 Karpathy 的 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 模式构建的个人知识库。

> 知识编译一次，持续更新——而不是每次查询重新从原始文档推导。

## 这是什么

一个用 LLM（Claude Code）维护的"第二大脑"：原始素材（书/课程）放 `raw/`，提炼后的概念、作者、领域聚合页放 `wiki/`。目标是让阅读和思考持续复利。

## 目录结构

| 路径 | 内容 | 谁维护 |
|------|------|--------|
| `raw/` | 原始素材（Wolai 导出的书/卡片，正文不可改） | 你 |
| `wiki/concepts/` | 概念、思想、框架（一概念一页） | Claude Code |
| `wiki/sources/` | 每本书/课程的摘要页 | Claude Code |
| `wiki/authors/` | 作者/思想家页 | Claude Code |
| `wiki/domains/` | 领域聚合页（每个概念一句话） | Claude Code |
| `wiki/meta/dashboard.md` | Obsidian Dataview 动态仪表盘 | 自动生成 |
| `CLAUDE.md` | Claude Code 行为规范（Schema） | 你 + Claude Code |

## 核心原则：概念筛选三原则

知识库只进"金子"。一个概念入选前，跑三问（详见 [[概念筛选三原则]]）：

1. **反直觉**——它纠正了我某个直觉错误吗？
2. **可迁移**——我能在它原本领域之外用它吗？
3. **可运算**——它给了我一个思考步骤，而不只是个标签/态度吗？

三项全过才建页面，否则不纳入。

## 怎么用

- **添加新书/卡片**：素材放 `raw/books/` 或 `raw/cards/` → 对 Claude Code 说「摄入《书名》」
- **提问**：直接问 Claude Code，好的回答会保存为 wiki 页面
- **检查**：说「检查 wiki」跑 lint（死链 / 孤立页 / frontmatter）

## 工具

- **Obsidian** + 插件：
  - **Dataview** — 动态仪表盘（`wiki/meta/dashboard.md`）
  - **Templater** — 新笔记模板
  - **Obsidian Git** — 自动 git 备份
  - **Linter** — 保存时自动把 frontmatter 的 `updated` 刷成当前时刻（规则 `YAML Timestamp`：key=`updated`、format=`YYYY-MM-DD HH:mm:ss`），让 `updated` 始终等于文件 mtime（精确到秒），零手动维护
- **Claude Code** — 维护 `wiki/` 下所有文件（创建、更新、删除、清理双链），编辑时同步写 `updated`

## 历史

2026-06 从 Wolai 迁移而成。
