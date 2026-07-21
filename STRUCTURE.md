# Project Structure Specification

> 本仓库目录约定、命名规则、文件分类、README 要求的总纲。
> **本地文件，no_git**，不入 git。本地修改即可，无需 commit。
> CLAUDE.md §6 末尾指引到本文件。

---

## §1. 顶层目录职责

| 目录 | 职责 | 是否入仓 |
|------|------|----------|
| `.claude/` | Claude Code 配置、AI 协作产物（rules/skills/scripts） | 是 |
| `.git/` | Git 内部数据 | — |
| `docs/` | 对外文档 + AI 协作过程产物（plans/sdd/superpowers） | 是 |
| 根文件 | `CLAUDE.md` `README.md` `CONTRIBUTING.md` `LICENSE` | 是 |
| 根 `STRUCTURE.md` | 本文件，规范总纲 | **否（no_git）** |

## §2. `.claude/` 内部

| 子目录 | 职责 |
|--------|------|
| `rules/common/` | 编码规范、测试、安全等通用 rules（与全局 ~/.claude/rules/common/ 同步镜像） |
| `skills/<name>/SKILL.md` | 项目私有 skill，每个 skill 一个目录，入口固定为 `SKILL.md` |
| `scripts/` | 项目私有脚本（占位） |
| `settings.json` | Claude Code 项目级配置（启用插件等） |
| `README.md` | `.claude/` 索引与维护说明（no_git） |

## §3. `docs/` 内部

| 子目录 | 职责 |
|--------|------|
| `principles.md` | 协作原则（计划本质、commit 节奏等） |
| `methodology.md` | Skill 沉淀方法论 |
| `plans/YYYY-MM-DD-<topic>.md` | 实施性 plan 文档（commit 入仓） |
| `plans/README.md` | plans 工作流说明（no_git） |
| `sdd/task-*.md` `review-*.md` `progress.md` | SDD（spec-driven development）过程产物（commit 入仓） |
| `sdd/README.md` | sdd 目录索引（no_git） |
| `superpowers/specs/*.md` | superpowers 类规格设计文档（commit 入仓） |
| `superpowers/README.md` | superpowers 目录索引（no_git） |
| `README.md` | `docs/` 总索引（no_git） |

## §4. 文件分类规则

- **commit 入仓**：所有正式文档、代码、配置、plan、sdd 过程产物
- **no_git（本地存在不入仓）**：
  - `STRUCTURE.md`（根总纲）
  - 各规范类 README（`.claude/README.md`、`docs/README.md`、`docs/plans/README.md`、`docs/sdd/README.md`、`docs/superpowers/README.md`）
- **no_git 机制**：`.gitignore` 模式精确匹配路径

## §5. 命名约定

> ⚠️ **暂未限定**。等重写阶段再讨论。当前观察到的现状：
> - 目录：kebab-case（`obsidian-vault-enhance`、`docs/sdd`）
> - 文件：kebab-case 为主，部分约定俗成保留 UPPERCASE（`SKILL.md`、`README.md`）
> - plan：`YYYY-MM-DD-<topic>.md`
> - sdd task：`task-<n>-<kind>.md`（`brief` / `report`）

## §6. README 要求

| 目录 | README | 类型 |
|------|--------|------|
| 根 | — | （用 `STRUCTURE.md` 代替总纲） |
| `.claude/` | `README.md` | no_git |
| `docs/` | `README.md` | no_git |
| `docs/plans/` | `README.md` | no_git |
| `docs/sdd/` | `README.md` | no_git |
| `docs/superpowers/` | `README.md` | no_git |

每个 README 应说明：本目录职责、子目录与文件列表、维护要点、与相邻目录的关系。

## §7. no_git 模式清单（维护用）

当前在 `.gitignore` 中：

```
/STRUCTURE.md
/.claude/README.md
/docs/README.md
/docs/sdd/README.md
/docs/superpowers/README.md
```

新增 no_git 文件时：在 `.gitignore` 末尾加一行精确路径。