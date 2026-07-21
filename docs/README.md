# `docs/` 目录说明

> 对外文档 + AI 协作过程产物（plans、sdd、superpowers specs）。
> **no_git**，本地修改即可。

## 定位说明

本仓库的核心产出是 `.claude/skills/`（沉淀的 skill）和 `.claude/rules/`（工作流规范）。
`plans/` 和 `sdd/` 是**本仓库自身建设的过程记录**，是方法论实跑的副产品。

| 文件/子目录 | 类型 | 说明 | 是否核心产出 |
|-------------|------|------|------------|
| `principles.md` | 文档（commit） | 协作原则 | ✅ 对外 |
| `methodology.md` | 文档（commit） | Skill 沉淀方法论 | ✅ 对外 |
| `plans/` | 过程产物（commit） | 实施性 plan 文档 | ❌ 副产品 |
| `sdd/` | 过程产物（commit） | SDD 任务与评审产物 | ❌ 副产品 |
| `superpowers/specs/` | 文档（commit） | superpowers 类规格设计 | ✅ 对外 |

## 维护要点

- `plans/` 文件命名：`YYYY-MM-DD-<topic>.md`
- `sdd/` 文件命名：`task-<n>-<brief|report>.md`、`review-<from>..<to>.diff`
- 各子目录有自己的 `README.md`（no_git）说明细节