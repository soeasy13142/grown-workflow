---
name: ecc-workflow
description: ECC 精选工作流 — 本仓库对 ECC（Enhanced Claude Capabilities）命令的封装与项目本地约定
---

# ecc-workflow

> 本 skill 基于 [ECC（affaan-m/ECC, MIT）](https://github.com/affaan-m/ECC) 的命令封装。ECC 是一套为 Claude Code 设计的工作流系统。
> 完整归属与许可证见 [CREDITS.md](../../../CREDITS.md)。

## 概述

本仓库从 ECC 中精选了 8 个核心命令，适配到本项目的上下文中。每个命令在 `.claude/skills/ecc-workflow/commands/` 下有独立的用法文档。

### 精选命令一览

| 命令 | 用途 | 文档 |
|------|------|------|
| `/ecc:plan` | 功能规划与任务拆解 | [ecc-plan](commands/ecc-plan.md) |
| `/tdd` | TDD 工作流 | [tdd](commands/tdd.md) |
| `/ecc:code-review` | 代码质量审查 | [ecc-code-review](commands/ecc-code-review.md) |
| `/ecc:build-fix` | 修复构建错误 | [ecc-build-fix](commands/ecc-build-fix.md) |
| `/ecc:refactor-clean` | 死代码清理 | [ecc-refactor-clean](commands/ecc-refactor-clean.md) |
| `/e2e` | 端到端测试 | [e2e](commands/e2e.md) |
| `/ecc:test-coverage` | 覆盖率分析 | [ecc-test-coverage](commands/ecc-test-coverage.md) |
| `/ecc:update-docs` | 文档更新 | [ecc-update-docs](commands/ecc-update-docs.md) |

### 如何使用

1. 确保 ECC 插件已安装（见 CLAUDE.md §2）
2. 在对话中直接键入上表命令
3. 首次使用某命令前，建议阅读对应的命令文档了解项目本地约定

### 约定

- **先 plan 再动手** — 跨多文件 / 多阶段的任务先用 `/ecc:plan`
- **TDD 优先** — 新功能走 `/tdd`，先测试再实现
- **合并前 review** — push 前走 `/ecc:code-review`
- **CC 声明** — commit message 末行附 `Co-Authored-By: Claude ...`
- **ECC 归属** — 所有基于 ECC 的对话产物在仓库中均通过 CREDITS.md 声明归属

---

*v0 — 精选自 ECC 的前 8 个高频命令。后续可根据项目需要增补。*
