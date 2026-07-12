# CLAUDE.md — grown-workflow AI 协作契约

> 本仓库的 AI 协作主契约。Claude Code 自动加载本文件。
> README.md 谈「为什么」，本文件谈「怎么做」。

## §0. 决策原则（最高优先级）

### 元规则：不确定 → 问，不替用户拍板

**触发**：任何时候遇到下列场景，**立即调用 AskUserQuestion**。一次问 1-4 个相关问题。

**禁止**：
- 「我假设你要的是 X」然后开干
- 「我选 A 因为…」直接执行，不等用户确认
- 把多个不确定点压成一个 silent decision
- 给「推荐选项」+「(Recommended)」后就跳过询问
- AI 可以列选项 + 推荐 + 理由，但**最终选择必须由人定**

### §0.1 AskUserQuestion 触发场景（按需对照）

> 下列 8 类场景中只要命中一条，**就问**。不要替用户判断「这个够清楚，可以直接做」——用户视角和 AI 视角不一致是常态。

| # | 场景 | 典型模糊输入 | 应问什么 |
|---|------|--------------|----------|
| 1 | **模糊动词/形容词** | 「帮我优化下」「重构一下」「改得更好」 | 优化哪个文件/函数/模块的哪方面？目标指标？ |
| 2 | **选型决策** | 「用啥库做 X」「哪个方案好」 | 列 ≥2 候选 + 推荐 + 各自理由，让用户挑 |
| 3 | **阈值与边界** | 「长函数」「大文件」「深嵌套」「复杂」 | 把抽象词换成具体数字选项（如 50 / 80 / 100 行） |
| 4 | **命名/标识符** | 「这个函数叫啥」「commit message 怎么写」 | 给 ≥2 命名候选 + 推荐，让用户定 |
| 5 | **范围与粒度** | 「改一下」「修一下 bug」 | 改一行 / 单文件 / 模块 / 全仓库？影响面多大？ |
| 6 | **风格与偏好** | 「按你想法写」「用合适的方式」 | 错误处理风格、注释密度、不可变程度、测试密度等 |
| 7 | **优先级/顺序** | 多个候选任务堆在一起 | 先做哪个？并行还是串行？ |
| 8 | **默认值/缺省行为** | 超时/重试/缓存/边界 fallback | 这种场景下默认行为用 A 还是 B？ |

**判断门槛**：宁可多问一次被嫌烦，也不要少问一次做错方向。「**稍有不清楚**」即触发。

---

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

本仓库精选了 [ECC](https://github.com/affaan-m/ECC)（Enhanced Claude Capabilities，MIT 许可证）的以下命令作为核心工作流。
> ECC 由 [affaan m](https://github.com/affaan-m) 开发，本仓库的使用和封装见 `CREDITS.md`。
> 详细项目本地约定见 `.claude/skills/ecc-workflow/SKILL.md`。

| 命令 | 何时用 | 项目本地文档 |
|------|--------|-------------|
| `/ecc:plan` | 功能规划与任务拆解 | [用法 →](.claude/skills/ecc-workflow/commands/ecc-plan.md) |
| `/tdd` | TDD 工作流 | [用法 →](.claude/skills/ecc-workflow/commands/tdd.md) |
| `/ecc:code-review` | 代码质量审查 | [用法 →](.claude/skills/ecc-workflow/commands/ecc-code-review.md) |
| `/ecc:build-fix` | 修复构建错误 | [用法 →](.claude/skills/ecc-workflow/commands/ecc-build-fix.md) |
| `/ecc:refactor-clean` | 死代码清理 | [用法 →](.claude/skills/ecc-workflow/commands/ecc-refactor-clean.md) |
| `/e2e` | 端到端测试 | [用法 →](.claude/skills/ecc-workflow/commands/e2e.md) |
| `/ecc:test-coverage` | 覆盖率分析 | [用法 →](.claude/skills/ecc-workflow/commands/ecc-test-coverage.md) |
| `/ecc:update-docs` | 文档更新 | [用法 →](.claude/skills/ecc-workflow/commands/ecc-update-docs.md) |

完整命令清单见 ECC 官方文档：https://github.com/affaan-m/ECC

## §3. Plans 工作流

- **触发条件：** 多文件 / 多阶段 / 跨多日 / 含架构决策 / 涉及不熟悉库
- **位置：** `docs/plans/YYYY-MM-DD-<topic>.md`
- **流程：** AskUserQuestion 确认范围 → 写 plan → 实施中持续更新 → 完成时回顾
- **原则：** plan 是活记录，不是出发前的门票（详见 `docs/principles.md`「计划的本质」）

简单任务（单文件、纯文档小改）不需要 plan。

## §4. DO（应该做的）

1. **AskUserQuestion 澄清** — 见 §0 元规则与 §0.1 触发场景表。任何需求里有不清楚、模糊、找不到、不知道选哪个的点，直接问。
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
14. **收到 skill 走方法论** — 用户提供任意形态 skill（句子/脚本/描述/workflow）时，按 `docs/methodology.md` 4 阶段流程整理：接收 → 疼痛溯源 → 沉淀 SKILL.md → 跑一次。不预设计，不跳过跑一次。

## §5. DON'T（不要做的）

### 决策类

1. **不要替用户拍板** — 见 §0 元规则。方向性、命名、选型、阈值、边界判断一律 AskUserQuestion。AI 可以列选项 + 推荐，但最终选择由人定。
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
- `docs/` — 对外文档（principles、plans、methodology、sdd、superpowers specs）
- `docs/methodology.md` — Skill 整理方法论 v0；`.claude/skills/<name>/SKILL.md` 按此整理
- **仓库根不放 `skills/`、`scripts/`**（已统一到 `.claude/` 下）
- **完整结构规范**（含目录命名、文件分类、README 要求、no_git 清单）见 `STRUCTURE.md`（本地文件，no_git，不入 git）。本节仅做要点提示。

### `docs/plans/` 与 `docs/sdd/` 的定位

> 本仓库的核心产出是 `.claude/skills/` 下的 skill 和 `.claude/rules/` 下的工作流规范。
> `docs/plans/` 和 `docs/sdd/` 是**本仓库自身建设的过程记录**，是方法论（plan 工作流、SDD）实跑的副产品，不属于要分享的核心内容。

| 目录 | 定位 | 是否核心产出 |
|------|------|------------|
| `.claude/skills/` | 沉淀的 skill 成果物 | ✅ |
| `.claude/rules/` | 工作流规范、编码规范 | ✅ |
| `docs/plans/` | plan 工作流建设本仓库的规划文档 | ❌ 副产品 |
| `docs/sdd/` | SDD 方法论建设本仓库的过程记录 | ❌ 副产品 |
| `docs/principles.md`、`docs/methodology.md` | 对外分享的方法论文档 | ✅ 对外 |

## §7. 与现有 rules 的关系

本文件补充 `~/.claude/rules/` 全局规则之上，**不替代**。

`.claude/rules/common/` 内是通用编码规范补充（coding-style、testing、security 等），详见各文件。
