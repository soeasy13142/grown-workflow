# grown-workflow AI 协作脚手架初始化 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 为 grown-workflow 仓库建立 AI 协作基础设施——根 CLAUDE.md、docs/plans/ 文件夹、.claude/skills/ 与 .claude/scripts/ 收纳，以及 README/CONTRIBUTING 的相关引用与细则。

**Architecture:** 单一文档（CLAUDE.md，~300-400 行）收纳本项目 AI 协作契约；plans 文件夹承担实施性 plan 文档；Claude Code 内部协作产物（skill 脚本）收纳到 `.claude/` 下，与对外文档分离。沿用 CONTRIBUTING.md 既有的「一次一个意图」节奏，本地高频提交、push 前整理。

**Tech Stack:** Markdown, Git, Claude Code + ECC 插件（`ecc@ecc`）。

## Global Constraints

- **Git 提交粒度：** 一次 commit 一个意图（沿用 CONTRIBUTING.md）
- **本地 commit、push 时机由用户决定：** 本计划只生成 6 个本地 commit，不 push
- **语言：** 面向人类协作者的中文（项目 README、principles 已用中文；CLAUDE.md 沿用）
- **CLAUDE.md 风格：** 章节清晰、表格化命令速查、DO/DON'T 分组列出
- **现有 `.claude/rules/common/` 不动：** 本计划仅新增 .claude/skills/、.claude/scripts/，不修改 rules/
- **现有 `.claude/settings.json` 不动：** ECC 插件已正确启用
- **不编写实际 skill 代码：** 本计划仅建脚手架（.gitkeep 占位）

---

## File Structure

```
grown-workflow/
├── CLAUDE.md                          # 新增 (Task 4)
├── README.md                          # 修改 (Task 5) - 末尾加引用
├── CONTRIBUTING.md                    # 修改 (Task 6) - 加 push 细则
├── docs/
│   ├── plans/
│   │   ├── README.md                  # 新增 (Task 3) - plan 工作流说明
│   │   └── .gitkeep                   # 新增 (Task 3)
├── .claude/
│   ├── skills/
│   │   └── .gitkeep                   # 新增 (Task 1)
│   ├── scripts/
│   │   └── .gitkeep                   # 新增 (Task 1)
├── skills/                            # 删除 (Task 2)
└── scripts/                           # 删除 (Task 2)
```

各文件职责：
- `CLAUDE.md` — 本仓库 AI 协作契约（决策原则、git 频率、ECC 命令、DO/DON'T、目录约定）
- `docs/plans/README.md` — plans 文件夹使用说明（何时写、命名、模板、不要做）
- `README.md` — 在末尾增加指向 CLAUDE.md 的引用段
- `CONTRIBUTING.md` — 在末尾增加 push 前规范化细则
- `.claude/skills/.gitkeep` / `.claude/scripts/.gitkeep` — 占位，使空目录入版本控制

---

### Task 1: 新增 `.claude/skills/` 和 `.claude/scripts/` 脚手架

**Files:**
- Create: `.claude/skills/.gitkeep`
- Create: `.claude/scripts/.gitkeep`

**Interfaces:**
- Consumes: nothing (no prior task)
- Produces: 两个空目录入版本控制；为后续 Claude Code 内部 skill 与脚本预留位置

- [ ] **Step 1: 创建 `.claude/skills/.gitkeep`**

```bash
mkdir -p /Users/charliepan/Downloads/grown-workflow/.claude/skills
touch /Users/charliepan/Downloads/grown-workflow/.claude/skills/.gitkeep
```

- [ ] **Step 2: 创建 `.claude/scripts/.gitkeep`**

```bash
mkdir -p /Users/charliepan/Downloads/grown-workflow/.claude/scripts
touch /Users/charliepan/Downloads/grown-workflow/.claude/scripts/.gitkeep
```

- [ ] **Step 3: 验证目录与文件存在**

```bash
ls -la /Users/charliepan/Downloads/grown-workflow/.claude/skills/
ls -la /Users/charliepan/Downloads/grown-workflow/.claude/scripts/
```

Expected: 两个目录均包含 `.gitkeep` 文件（输出包含 `.gitkeep` 行）。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add .claude/skills/ .claude/scripts/
git commit -m "chore: add .claude/skills/ and .claude/scripts/ scaffolds"
```

---

### Task 2: 删除仓库根 `skills/` 和 `scripts/`（已统一到 `.claude/` 下）

**Files:**
- Delete: `skills/` (含 `.gitkeep`)
- Delete: `scripts/` (含 `.gitkeep`)

**Interfaces:**
- Consumes: Task 1 已建 `.claude/skills/`、`.claude/scripts/`
- Produces: 仓库根不再有 `skills/`、`scripts/`；语义统一到 `.claude/` 下

- [ ] **Step 1: 用 git rm 删除仓库根 `skills/`**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git rm -r skills/
```

Expected: 输出 `rm 'skills/.gitkeep'`。

- [ ] **Step 2: 用 git rm 删除仓库根 `scripts/`**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git rm -r scripts/
```

Expected: 输出 `rm 'scripts/.gitkeep'`。

- [ ] **Step 3: 验证删除**

```bash
ls /Users/charliepan/Downloads/grown-workflow/ | grep -E "^(skills|scripts)$"
```

Expected: 无输出（仓库根不再有 skills/、scripts/）。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git commit -m "chore: remove root skills/ and scripts/ (consolidated into .claude/)"
```

---

### Task 3: 新增 `docs/plans/` 文件夹及 README 模板

**Files:**
- Create: `docs/plans/.gitkeep`
- Create: `docs/plans/README.md`

**Interfaces:**
- Consumes: nothing
- Produces: plans 文件夹与说明文档；为后续实施性 plan 提供位置与模板

- [ ] **Step 1: 创建 `docs/plans/.gitkeep`**

```bash
mkdir -p /Users/charliepan/Downloads/grown-workflow/docs/plans
touch /Users/charliepan/Downloads/grown-workflow/docs/plans/.gitkeep
```

- [ ] **Step 2: 创建 `docs/plans/README.md`，内容如下**

写入文件 `/Users/charliepan/Downloads/grown-workflow/docs/plans/README.md`，内容为：

````markdown
# Plans

复杂任务的 plan 文档存放处。Plan 是活记录，不是出发前的门票。

## 何时写 plan

满足以下任一条件：

- 跨多文件
- 多阶段（分析 → 设计 → 实施 → 验证）
- 跨多日
- 含架构决策
- 涉及不熟悉的库 / 框架 / API

## 命名

`YYYY-MM-DD-<topic>.md`，例如 `2026-07-10-claude-md-init.md`。

## 模板

1. 目标（一句话）
2. 范围（做什么 / 不做什么）
3. 步骤
4. 决策记录（实施中改了什么、为什么）
5. 回顾（完成后）

## 不要做

- 不要把 plan 写进 CLAUDE.md 或其他文件
- 不要在 plan 之外的地方藏代码片段
- 不要 plan 与实施脱钩——plan 是活记录，改 plan 是正常的
````

（用 Write 工具创建。文件内容已在上方。）

- [ ] **Step 3: 验证文件内容**

```bash
head -5 /Users/charliepan/Downloads/grown-workflow/docs/plans/README.md
```

Expected: 首 5 行包含 `# Plans` 与 `## 何时写 plan`。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add docs/plans/
git commit -m "docs: add docs/plans/ with README template"
```

---

### Task 4: 新增仓库根 `CLAUDE.md`（AI 协作契约）

**Files:**
- Create: `CLAUDE.md`

**Interfaces:**
- Consumes: 无（不依赖前序任务的产出）
- Produces: 仓库根 CLAUDE.md，Claude Code 自动加载；含 §0-§7 共 8 节

- [ ] **Step 1: 创建 `CLAUDE.md`，完整内容如下**

写入文件 `/Users/charliepan/Downloads/grown-workflow/CLAUDE.md`，内容为：

````markdown
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
| `/ecc:tdd` | TDD 工作流 |
| `/ecc:code-review` | 代码质量审查 |
| `/ecc:build-fix` | 修复构建错误 |
| `/ecc:refactor-clean` | 死代码清理 |
| `/ecc:e2e` | 端到端测试 |
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
9. **测试驱动** — 新功能走 `/ecc:tdd`，先写测试再写实现。
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
````

（用 Write 工具创建。文件内容已在上方。）

- [ ] **Step 2: 验证 CLAUDE.md 包含 8 节标题**

```bash
grep -E "^## §" /Users/charliepan/Downloads/grown-workflow/CLAUDE.md
```

Expected: 输出 8 行，分别为 `§0.` 到 `§7.`。

- [ ] **Step 3: 验证行数在合理范围**

```bash
wc -l /Users/charliepan/Downloads/grown-workflow/CLAUDE.md
```

Expected: 300-450 行。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add CLAUDE.md
git commit -m "docs: add CLAUDE.md (AI collaboration contract)"
```

---

### Task 5: 在 README.md 末尾增加指向 CLAUDE.md 的引用段

**Files:**
- Modify: `README.md`（末尾追加，不修改既有内容）

**Interfaces:**
- Consumes: Task 4 产出的 CLAUDE.md
- Produces: README.md 末尾新增一节，链接到 CLAUDE.md

- [ ] **Step 1: 在 `README.md` 末尾追加以下内容**

在文件 `/Users/charliepan/Downloads/grown-workflow/README.md` 的**末尾**追加（用 Edit 工具，old_string 为文件现有最后一段，new_string 为「现有末尾 + 新增内容」）：

````markdown


## 附：给 AI 协作者的契约

本仓库的 AI 协作主契约在 [`CLAUDE.md`](./CLAUDE.md)。Claude Code 在本仓库内工作时自动加载该文件。涉及决策、git 流程、ECC 命令、DO/DON'T 等协作约定，以 `CLAUDE.md` 为准。
````

追加后，最后几行应为：

```
... (原有内容) ...

## 附：给 AI 协作者的契约

本仓库的 AI 协作主契约在 [`CLAUDE.md`](./CLAUDE.md)。Claude Code 在本仓库内工作时自动加载该文件。涉及决策、git 流程、ECC 命令、DO/DON'T 等协作约定，以 `CLAUDE.md` 为准。
```

- [ ] **Step 2: 验证追加成功**

```bash
tail -5 /Users/charliepan/Downloads/grown-workflow/README.md
```

Expected: 末 5 行包含 `## 附：给 AI 协作者的契约`。

- [ ] **Step 3: 验证 README 主体内容未被改动（行数应略增）**

```bash
wc -l /Users/charliepan/Downloads/grown-workflow/README.md
```

Expected: 比修改前略增（约 +5 行）。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add README.md
git commit -m "docs: link README.md to CLAUDE.md"
```

---

### Task 6: 在 CONTRIBUTING.md 末尾补充 push 规范化细则

**Files:**
- Modify: `CONTRIBUTING.md`（末尾追加，不修改既有内容）

**Interfaces:**
- Consumes: Task 1-4 已就位的脚手架
- Produces: CONTRIBUTING.md 含 git push 前 squash / rebase 流程

- [ ] **Step 1: 在 `CONTRIBUTING.md` 末尾追加以下内容**

在文件 `/Users/charliepan/Downloads/grown-workflow/CONTRIBUTING.md` 的**末尾**追加：

````markdown


## Git Push 规范化

本地提交按 `一次一个意图` 的节奏进行（高频、小颗粒）。push 到远端前必须整理 commit 历史：

### 推荐流程

```bash
# 1. 确认 main 是最新的
git fetch origin
git checkout main
git pull --rebase

# 2. 切到你的功能分支，整理 commit
git checkout feature/your-branch
git rebase -i main
# 把除第一个外的 commit 标记为 squash / fixup

# 3. 推送（首次推送加 -u）
git push -u origin feature/your-branch

# 或合并到 main（merge 模式任选，建议 fast-forward 或 squash merge）
```

### 原则

- push 出去的 commit 列表应是一个连贯的「意图批次」，不是本地细粒度 commit 流
- push 前自查：`git log origin/main..HEAD` 应是可独立检视的几个 commit
- 如果一个功能分支上本地有 10+ 个 commit，先 rebase 整理，再 push
````

追加后，最后几行应为：

```
... (原有内容) ...

## Git Push 规范化

本地提交按 `一次一个意图` 的节奏进行（高频、小颗粒）...
```

- [ ] **Step 2: 验证追加成功**

```bash
tail -5 /Users/charliepan/Downloads/grown-workflow/CONTRIBUTING.md
```

Expected: 末 5 行包含 `## Git Push 规范化`。

- [ ] **Step 3: 验证 CONTRIBUTING 主体内容未被改动**

```bash
wc -l /Users/charliepan/Downloads/grown-workflow/CONTRIBUTING.md
```

Expected: 比修改前略增（约 +30 行）。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add CONTRIBUTING.md
git commit -m "docs: detail git push normalization in CONTRIBUTING.md"
```

---

## 验收标准（整体）

执行全部 6 个任务后，验证：

- [ ] 仓库根存在 `CLAUDE.md`，含 `§0` 到 `§7` 共 8 节
- [ ] `docs/plans/README.md` 存在且含「何时写 plan」「命名」「模板」「不要做」四节
- [ ] `.claude/skills/.gitkeep` 与 `.claude/scripts/.gitkeep` 存在
- [ ] 仓库根 `skills/`、`scripts/` 已不存在
- [ ] `README.md` 末尾包含「附：给 AI 协作者的契约」段
- [ ] `CONTRIBUTING.md` 末尾包含「Git Push 规范化」段
- [ ] git log 显示 6 个新 commit（commit 1-6）

```bash
# 最终验证
cd /Users/charliepan/Downloads/grown-workflow
git log --oneline -10
ls CLAUDE.md docs/plans/README.md .claude/skills/.gitkeep .claude/scripts/.gitkeep
ls skills/ scripts/ 2>&1 | grep -E "No such"  # 应有 No such file or directory
```

预期：6 个新 commit 的 subject 分别为：
- `chore: add .claude/skills/ and .claude/scripts/ scaffolds`
- `chore: remove root skills/ and scripts/ (consolidated into .claude/)`
- `docs: add docs/plans/ with README template`
- `docs: add CLAUDE.md (AI collaboration contract)`
- `docs: link README.md to CLAUDE.md`
- `docs: detail git push normalization in CONTRIBUTING.md`

**不要 push。** push 时机由用户决定。
