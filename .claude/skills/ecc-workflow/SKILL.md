---
name: ecc-workflow
description: ECC 精选工作流 — 本仓库对 ECC（Enhanced Claude Capabilities）命令的封装与项目本地约定
status: v0
---

# ecc-workflow

> 本 skill 基于 [ECC（affaan-m/ECC, MIT）](https://github.com/affaan-m/ECC) 的命令封装。ECC 是一套为 Claude Code 设计的工作流系统。
> 完整归属与许可证见 [CREDITS.md](../../../CREDITS.md)。  ✅ v0 · 2026-07-10

## ECC 命令编排

本仓库精选的 8 个 ECC 命令可以串联成一个完整的工作流，从任务规划到最终推送：

```mermaid
flowchart LR
    Start([新任务]) --> Plan[/ecc:plan]
    Plan --> TDD{需要新功能？}
    TDD -->|是| TDDProc[/tdd]
    TDD -->|否| Code[/ecc:code-review]
    TDDProc --> Code
    Code --> Fix{有问题？}
    Fix -->|构建错误| BuildFix[/ecc:build-fix]
    Fix -->|死代码/异味| Refactor[/ecc:refactor-clean]
    BuildFix --> Code
    Refactor --> Code
    Fix -->|通过| E2E{需要端到端？}
    E2E -->|是| E2EProc[/e2e]
    E2E -->|否| Coverage[/ecc:test-coverage]
    E2EProc --> Coverage
    Coverage --> Doc{文档需更新？}
    Doc -->|是| DocUp[/ecc:update-docs]
    Doc -->|否| Push([git push])
    DocUp --> Push

    classDef cmd fill:#cce5ff,stroke:#007bff,color:#000
    class Plan,TDDProc,Code,BuildFix,Refactor,E2EProc,Coverage,DocUp cmd
```

## 场景速查

| 你的场景 | 起点命令 | 可能还需要 |
|----------|---------|-----------|
| 做一个新功能 | `/ecc:plan` → `/tdd` | `/ecc:code-review` → `/ecc:test-coverage` |
| 修一个 bug | `/ecc:plan` | `/ecc:code-review` → `/ecc:build-fix` |
| 只想 review 当前改动 | `/ecc:code-review` | `/ecc:refactor-clean`（如有死代码） |
| 重构/清理代码 | `/ecc:refactor-clean` | `/ecc:code-review` |
| 发布前全量检查 | `/e2e` → `/ecc:test-coverage` | `/ecc:update-docs` |
| 修复构建错误 | `/ecc:build-fix` | `/ecc:code-review` |

## 精选命令一览

| 命令 | 用途 | 文档 | 版本 |
|------|------|------|------|
| `/ecc:plan` | 功能规划与任务拆解 | [ecc-plan](commands/ecc-plan.md) | ✅ v0 |
| `/tdd` | TDD 工作流 | [tdd](commands/tdd.md) | ✅ v0 |
| `/ecc:code-review` | 代码质量审查 | [ecc-code-review](commands/ecc-code-review.md) | ✅ v0 |
| `/ecc:build-fix` | 修复构建错误 | [ecc-build-fix](commands/ecc-build-fix.md) | ✅ v0 |
| `/ecc:refactor-clean` | 死代码清理 | [ecc-refactor-clean](commands/ecc-refactor-clean.md) | ✅ v0 |
| `/e2e` | 端到端测试 | [e2e](commands/e2e.md) | ✅ v0 |
| `/ecc:test-coverage` | 覆盖率分析 | [ecc-test-coverage](commands/ecc-test-coverage.md) | ✅ v0 |
| `/ecc:update-docs` | 文档更新 | [ecc-update-docs](commands/ecc-update-docs.md) | ✅ v0 |

## 如何使用

1. 确保 ECC 插件已安装（见 CLAUDE.md §2）
2. 不确定从哪个命令开始时，参考上方的**场景速查表**
3. 首次使用某命令前，建议阅读对应的命令文档了解项目本地约定

## 约定

- **先 plan 再动手** — 跨多文件 / 多阶段的任务先用 `/ecc:plan`
- **TDD 优先** — 新功能走 `/tdd`，先测试再实现
- **合并前 review** — push 前走 `/ecc:code-review`
- **CC 声明** — commit message 末行附 `Co-Authored-By: Claude ...`
- **ECC 归属** — 所有基于 ECC 的对话产物在仓库中均通过 CREDITS.md 声明归属
- **每完成一次 ECC 命令调用** — 在对话末尾追加交接记录，风格参考本仓库的 `CREDITS.md` 和项目交接文档做法

## 边界与陷阱

| 情况 | 处理 |
|------|------|
| 不确定用哪个命令 | 看**场景速查表**，或直接用 AskUserQuestion 问用户 |
| 命令执行结果不符合预期 | 描述偏差，ECC 会调整；必要时人工介入 |
| ECC 不可用（网络/插件问题） | 降级到手工流程：手工 plan → 手工 review → ... |
| 多个命令串起来不顺畅 | 看编排图找卡点，或跳到 `/ecc:code-review` 做统一审查 |

## 使用情况跟踪

> 暂无实跑记录——本 skill 刚刚从设计阶段升级完成，后续每次调用在此追加记录。

---

## 已知不足（v0）

- 精选范围仅为 ECC 278 个 skill 中的 8 个命令，其他命令未被覆盖
- ECC 版本更新的命令行为变更，本文档可能滞后
- 场景速查表仅覆盖常见场景，非常见任务类型可能需要探索式使用
- 使用情况跟踪尚未开启，缺少实际调用数据驱动优化

## 历史

- 2026-07-10: v0 从 ECC 精选纳入，首次提交（commit `d12eef9`）
- 2026-07-10: v0 深度升级——加 Mermaid 编排图、场景速查表、边界与陷阱、已知不足

## 参考

- [ECC 官方仓库](https://github.com/affaan-m/ECC)
- [CREDITS.md](../../../CREDITS.md) — 归属与许可证
- [CLAUDE.md §2](../../../CLAUDE.md) — ECC 命令速查
- [obsidian-vault-enhance SKILL.md](../obsidian-vault-enhance/SKILL.md) — 本仓库 skill 风格参考
