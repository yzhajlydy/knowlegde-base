# 个人知识库 Wiki

基于 Karpathy 的 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 模式构建的个人知识库。

## 核心理念

> 知识编译一次，持续更新 —— 而不是每次查询重新从原始文档推导。

## 快速开始

1. 用 Obsidian 打开此目录作为 Vault
2. 安装推荐插件：Dataview、Templater、Obsidian Git
3. 在 Obsidian 设置中启用 CSS Snippet：`vault-colors`
4. 开始使用！

## 目录说明

| 目录 | 说明 | 谁负责 |
|------|------|--------|
| `raw/` | 原始素材（不可变） | 你维护 |
| `wiki/` | LLM 生成的知识库 | Claude Code 维护 |
| `CLAUDE.md` | 行为规范（Schema） | 你和 Claude Code 共同迭代 |

## 日常使用

- **添加新书**：笔记放入 `raw/books/` → 在 Claude Code 中说"摄入 [书名]"
- **添加文章**：用 Obsidian Web Clipper 保存到 `raw/articles/` → 摄入
- **提问**：直接在 Claude Code 中提问 → 好的回答会保存为 wiki 页面
- **检查**：每摄入 15-20 个素材后运行一次 lint

## Obsidian 推荐插件

- **Dataview** — YAML frontmatter 数据查询
- **Templater** — 新笔记模板
- **Obsidian Git** — 自动 git 备份
- **Calendar** — 日历视图
- **Obsidian Web Clipper** — 浏览器剪藏

## 迁移指南

### 从 Wolai 迁移知识卡片

1. 在 Wolai 中选中知识卡片
2. 导出为 Markdown（或 HTML 后用 pandoc 转换）：
   ```bash
   pandoc input.html -t markdown -o output.md
   ```
3. 将导出文件放入 `raw/cards/`
4. 在 Claude Code 中说"摄入 Wolai 知识卡片"
5. Claude Code 会逐批处理（每批 10 张），为每张卡片：
   - 创建对应的 `wiki/concepts/` 页面
   - 添加 frontmatter（type, domain, tags）
   - 用 wikilinks 重建卡片之间的关联
   - 更新 index.md 和 log.md

### 从 Wolai 迁移读书笔记

1. 将 Wolai 中的读书笔记导出
2. 按系列/作者分目录放入 `raw/books/`
3. 在 Claude Code 中逐本摄入：
   ```
   摄入《经济学讲义》
   ```
4. Claude Code 会自动创建来源摘要页、提取概念、更新领域页

### 建议的迁移顺序

1. 先迁移 5-10 张知识卡片做试运行，验证流程
2. 批量迁移剩余知识卡片
3. 从已读书籍开始迁移（优先选择笔记最完整的）
4. 未读书籍在阅读后再摄入

## 版本管理

```bash
# 查看最近活动
grep "^## \[" wiki/log.md | head -10

# Git 历史
git log --oneline -10
```
