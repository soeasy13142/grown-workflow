# CLAUDE.md — grown-workflow AI 协作契约

> 本仓库的 AI 协作主契约。Claude Code 自动加载本文件。
> README.md 谈「为什么」，本文件谈「怎么做」。

## §0. 决策原则（最高优先级）

- **任何不清楚、模糊、不确定、不知道选哪个 → 直接用 AskUserQuestion 问，不要替我做决策。**
- 复杂任务（跨多文件 / 多阶段 / 跨多日）→ 先写 plan，再实施。
- 拍板权不可委托：让 AI 替你定方向是反模式。

## §1. Git 提交频率规范

- **本地提交：** 高频、一次一个意图（沿用 CONTRIBUTING.md）。
- **Push 前：** 必须先 rebase/squash 合并，整理 commit 历史。
- **合并粒度：** 每个 push 的 commit 列表应是一个连贯的「意图批次」，而不是本地高频的细粒度 commit 流。

常用整理命令：

```bash
# 整理最近 N 个 commit
git rebase -i HEAD~N

# 把分支上所有 commit 合并成一个（适合「本地高频、push 前 squash」场景）
git rebase -i <base-branch>
# 然后把除第一个外的所有 commit 标记为 squash / fixup
```

## §2. ECC 命令速查

本项目强制使用 ECC 插件（已在 `.claude/settings.json` 启用 `ecc@ecc`）。
最常用的 8 个命令：

| 命令 | 何时用 |
|------|--------|
| `/ecc:plan` | 功能规划与任务拆解 |
| `/tdd` | TDD 工作流 |
| `/ecc:code-review` | 代码质量审查 |
| `/ecc:build-fix` | 修复构建错误 |
| `/ecc:refactor-clean` | 死代码清理 |
| `/e2e` | 端到端测试 |
| `/ecc:test-coverage` | 覆盖率分析 |
| `/ecc:update-docs` | 文档更新 |

完整命令清单见 ECC 官方文档：https://github.com/affaan-m/ECC

## §3. Plans 工作流

- **触发条件：** 多文件 / 多阶段 / 跨多日 / 含架构决策 / 涉及不熟悉库
- **位置：** `docs/plans/YYYY-MM-DD-<topic>.md`
- **流程：** AskUserQuestion 确认范围 → 写 plan → 实施中持续更新 → 完成时回顾
- **原则：** plan 是活记录，不是出发前的门票（详见 `docs/principles.md`「计划的本质」）

简单任务（单文件、纯文档小改）不需要 plan。

## §4. DO（应该做的）

1. **用 AskUserQuestion 澄清** — 任何需求里有不清楚、模糊、找不到、不知道选哪个的点，直接问。一次问 1-4 个相关问题。
2. **复杂任务先写 plan** — 满足 §3 触发条件时，先在 `docs/plans/` 写 plan，实施中持续更新，完成时附回顾。
3. **本地提交高频、一次一个意图** — 沿用 CONTRIBUTING.md。commit message 写明意图，不混多个意图。
4. **Push 前先合并** — `git rebase -i` 或 `git merge --squash`，把本地多个细粒度 commit 整理成「意图批次」。
5. **用 ECC 命令** — §2 列出的命令是本项目首选入口，不用手工拼凑等价流程。
6. **库文档查 Context7** — 涉及具体库/框架/API 时用 Context7 MCP，不走 WebSearch。
7. **并行任务用并行 Agent** — 独立任务并行调度，不要串行等待。
8. **改动完成请求 code-review** — 走 `/ecc:code-review` 或 `code-reviewer` Agent。
9. **测试驱动** — 新功能走 `/tdd`，先写测试再写实现。
10. **错误显式处理** — 不 swallow errors；UI 层用友好消息，服务层记详细上下文。
11. **不可变数据** — update 不 mutate，改写时返回新对象。
12. **输入边界验证** — 系统边界处用 schema 验证，失败快速失败。
13. **Secrets 走环境变量** — 不硬编码；启动时校验必需 env 已设置。

## §5. DON'T（不要做的）

### 决策类

1. **不要替我拍板** — 任何方向性、命名、选型、阈值、边界判断，一律 AskUserQuestion。AI 可以列选项 + 推荐，但最终选择由人定。
2. **不要假设需求** — 含糊的需求先确认，不要「按我理解」开干。「我以为你要的是 X」是协作头号反模式。

### 流程类

3. **不要跳过 plan** — 满足 §3 触发条件时直接动手是反模式。即使 plan 很简单，也要在 `docs/plans/` 留一份。
4. **不要混合意图 commit** — 一个 commit 只做一件事。「顺便改一下命名」是常见反模式，会被迫拆 commit 或回滚。
5. **不要未经合并直接 push** — push 出去的 commit 应是「意图批次」，不是本地高频细粒度的 commit 流。
6. **不要跳过 code-review** — 主分支 / 共享分支的合并前必须有 review；走 `/ecc:code-review` 或 `code-reviewer` Agent。

### 信息获取类

7. **不要用 WebSearch 查库文档** — 用 Context7 MCP。WebSearch 仅用于 Context7 查不到或非库类信息。
8. **不要凭记忆写库 API** — 即使是熟悉库，也走 Context7 验证。训练数据可能与最新版本脱节。

### 代码质量类

9. **不要写长函数（>50 行）** — 拆成 <50 行的子函数。
10. **不要写超大文件（>800 行）** — 按职责拆模块。
11. **不要深度嵌套（>4 层）** — 用 early return 改写。
12. **不要用 mutation 模式** — 改数据返回新对象，不原地改。KISS/DRY/YAGNI 见 `.claude/rules/common/coding-style.md`。
13. **不要硬编码 secrets** — 用环境变量或 secret manager。启动时校验必需 env 已存在。

### 错误与可观测性

14. **不要默默吞错误** — 错误必须显式处理或显式抛出。`catch (e) {}` 是反模式。
15. **不要留 console.log / debug 痕迹** — 提交前清理调试代码。

### 测试与覆盖率

16. **不要跳过测试** — 新功能必须有测试，目标覆盖率 ≥ 80%（见 `.claude/rules/common/testing.md`）。不要写测试仅为通过覆盖率而非真实覆盖行为。

### 提交安全

17. **不要提交敏感数据** — API key、密码、token、私钥、个人隐私。见 `.claude/rules/common/security.md`。

## §6. 目录约定

- `.claude/` — Claude Code 配置 + AI 协作产物（plans、skills、scripts、rules）
- `docs/` — 对外文档（principles、plans）
- **仓库根不放 `skills/`、`scripts/`**（已统一到 `.claude/` 下）

## §7. 与现有 rules 的关系

本文件补充 `~/.claude/rules/` 全局规则之上，**不替代**。

`.claude/rules/common/` 内是通用编码规范补充（coding-style、testing、security 等），详见各文件。
