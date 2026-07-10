# 命令：`/ecc:update-docs` — 文档更新

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:update-docs`。详见 [CREDITS.md](../../../CREDITS.md)。

## 何时用

- 代码变更后文档不同步
- 新增功能需要补充文档
- API / 接口签名变更
- README 或 CLAUDE.md 需要同步更新

## 本仓库约定

1. **文档即代码** — 文档变更和代码变更在同一个 commit 中（不单独开"补文档"commit）
2. **CLAUDE.md §6 目录约定** — 外部文档走 `docs/`，AI 协作产物走 `.claude/`
3. **归属声明不可省略** — 引用外部项目时，在 `CREDITS.md` 中记录

## 用法

```
在对话中直接输入：
/ecc:update-docs
```

ECC 会对比代码变更和现有文档，列出需要更新的部分。

## 本仓库文档体系

| 层级 | 文件 | 内容 |
|------|------|------|
| 顶层 | `README.md` | 项目定位、母题、快速开始 |
| 契约 | `CLAUDE.md` | AI 协作规则 |
| 方法论 | `docs/methodology.md` | Skill 整理方法论 |
| 原则 | `docs/principles.md` | 深层设计原则 |
| Plan | `docs/plans/` | 功能规划文档 |
| Skill | `.claude/skills/` | 可复用 skill 定义 |
| 归属 | `CREDITS.md` | 外部项目和参考来源 |

---

*v0 — 适配 grown-workflow 的文档更新约定。*
