# Project Structure Normalization Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 规范化 grown-workflow 项目结构——合并 `.superpowers/sdd/` 到 `docs/` 下、补齐各子目录 README、写根 `STRUCTURE.md` 总纲、`CLAUDE.md §6` 加 cross-ref。**规范类文件**（`STRUCTURE.md` 与子目录 README）走 `no_git` 机制（.gitignore 排除），本地存在但不入仓；迁移与 `.gitignore`/`CLAUDE.md` 改动正常 commit。

**Architecture:**
- **物理层（committed）** — 目录迁移、`.gitignore` 模式、`CLAUDE.md` 指引行
- **文档层（no_git）** — `STRUCTURE.md` 总纲 + 各子目录 README，本地可达、不入 git
- **职责收敛** — SDD 过程产物统一进 `docs/sdd/`；`.superpowers/` 是工具副产品目录，迁完即删

**Tech Stack:** Markdown, Git, .gitignore

## Global Constraints

- **Git 提交粒度：** 一次 commit 一个意图（沿用 CONTRIBUTING.md）
- **本地 commit、push 时机由用户决定：** 不 push
- **no_git 文件不 commit：** STRUCTURE.md 与各子目录规范 README 由 .gitignore 排除，绝不入 commit 列表
- **命名约定暂不限定：** 用户决定「等重写阶段再谈」，STRUCTURE.md 只描述现状与待定项，不强加规则
- **不动 `docs/superpowers/`：** 用户决定「纯迁移，不动 docs/superpowers/」
- **不写脚本：** 全部操作直接用 `git mv` / `Write` / `Edit`，不引入新脚本
- **`.superpowers/sdd/` 本就不入仓（已知偏差，2026-07-11 实施时发现）：** 原目录内含 `.gitignore`（内容 `*`），22 个文件从未入过 git。本计划 Task 2 已据此修订：删子 `.gitignore` → `mv` → `git add` 入仓，而非 `git mv`。本次是首次把这些过程产物 commit 入仓。

---

## File Structure（变动后）

```
grown-workflow/
├── STRUCTURE.md                       # 新增 (Task 3) — no_git
├── CLAUDE.md                          # 修改 (Task 5) — §6 加 cross-ref
├── .gitignore                         # 修改 (Task 4) — 加 no_git 模式
├── docs/
│   ├── sdd/                           # 新增 (Task 2) — 从 .superpowers/sdd/ 迁来
│   │   ├── README.md                  # 新增 (Task 3) — no_git
│   │   ├── task-*.md
│   │   ├── review-*.md
│   │   └── progress.md
│   ├── README.md                      # 新增 (Task 3) — no_git
│   ├── superpowers/
│   │   ├── README.md                  # 新增 (Task 3) — no_git
│   │   └── specs/                     # 不动
├── .claude/
│   ├── README.md                      # 新增 (Task 3) — no_git
└── .superpowers/                      # 删除 (Task 2)
```

---

### Task 1: 写本 plan 到 `docs/plans/`

**Files:**
- Create: `docs/plans/2026-07-11-project-structure-normalization.md`

**Interfaces:**
- Consumes: nothing
- Produces: plan 文档入 `docs/plans/`，作为后续 4 个 task 的依据

- [ ] **Step 1: 写 plan 文件**（用 Write 工具，内容为本文件本身）

- [ ] **Step 2: 验证 plan 存在**

```bash
ls -la /Users/charliepan/Downloads/grown-workflow/docs/plans/2026-07-11-project-structure-normalization.md
```

Expected: 文件存在，权限正常。

- [ ] **Step 3: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add docs/plans/2026-07-11-project-structure-normalization.md
git commit -m "docs: add plan for project structure normalization"
```

---

### Task 2: 迁移 `.superpowers/sdd/` → `docs/sdd/`（首次入仓）

**Files:**
- Delete: `.superpowers/sdd/.gitignore`（阻止子目录入仓的 `*` 规则，本次不再需要）
- Move: `.superpowers/sdd/*` → `docs/sdd/`
- Add (git): `docs/sdd/*` 全部入仓
- Delete: `.superpowers/` (迁移后该目录应为空，再删)

**Interfaces:**
- Consumes: Task 1 完成的 plan
- Produces: SDD 过程产物从「本地不入仓」转为「入仓在 `docs/sdd/`」；`.superpowers/` 目录消失

> **与原 plan 的偏差：** 原 plan 假设 `git mv`，实际 `git mv` 因 `.superpowers/sdd/` 未被 git 追踪而失败。修订为「删子 .gitignore → 普通 mv → git add」。这是这 22 个文件的**首次入仓**。

- [ ] **Step 1: 删除子 `.gitignore`（解 gitignore）**

```bash
rm /Users/charliepan/Downloads/grown-workflow/.superpowers/sdd/.gitignore
```

Expected: 静默成功。`.superpowers/sdd/` 下应剩 23 个文件（不含隐藏 .gitignore）。

- [ ] **Step 2: 验证 .superpowers/sdd/ 当前文件数**

```bash
ls -A /Users/charliepan/Downloads/grown-workflow/.superpowers/sdd/ | wc -l
```

Expected: `23`（22 个文件 + 1 个 .DS_Store 可能，但本目录不应有 .DS_Store）。

- [ ] **Step 3: mv 目录到 docs/sdd/**

```bash
mv /Users/charliepan/Downloads/grown-workflow/.superpowers/sdd \
   /Users/charliepan/Downloads/grown-workflow/docs/sdd
```

Expected: 静默成功。`docs/sdd/` 出现，`.superpowers/sdd/` 不再存在。

- [ ] **Step 4: 删除空的 .superpowers/**

```bash
rmdir /Users/charliepan/Downloads/grown-workflow/.superpowers
```

Expected: 静默成功（若目录非空会报错，可改用 `rm -rf`）。

- [ ] **Step 5: 验证 docs/sdd/ 含全部 23 个文件**

```bash
ls /Users/charliepan/Downloads/grown-workflow/docs/sdd/ | wc -l
```

Expected: `23`。

- [ ] **Step 6: git add 入仓**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add docs/sdd/
```

Expected: 输出若干 `add 'docs/sdd/...'` 行（首次入仓）。

- [ ] **Step 7: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git commit -m "refactor: migrate .superpowers/sdd/ to docs/sdd/ (first commit)"
```

Expected: 一个新 commit，包含 23 个新文件。

---

### Task 3: 写 STRUCTURE.md 与各子目录 README（no_git，不 commit）

**Files:**
- Create: `STRUCTURE.md`（根）
- Create: `.claude/README.md`
- Create: `docs/README.md`
- Create: `docs/sdd/README.md`
- Create: `docs/superpowers/README.md`

**Interfaces:**
- Consumes: Task 2 已完成的目录迁移
- Produces: 总纲 + 4 个子目录 README，本地可达

> **注意：** 这 5 个文件写完后**不要 commit**，由 Task 4 的 .gitignore 排除。

- [ ] **Step 1: 写根 `STRUCTURE.md`**

文件内容见下方「§ A. STRUCTURE.md 内容」。

- [ ] **Step 2: 写 `.claude/README.md`**

文件内容见下方「§ B. .claude/README.md 内容」。

- [ ] **Step 3: 写 `docs/README.md`**

文件内容见下方「§ C. docs/README.md 内容」。

- [ ] **Step 4: 写 `docs/sdd/README.md`**

文件内容见下方「§ D. docs/sdd/README.md 内容」。

- [ ] **Step 5: 写 `docs/superpowers/README.md`**

文件内容见下方「§ E. docs/superpowers/README.md 内容」。

- [ ] **Step 6: 验证文件存在**

```bash
ls -la /Users/charliepan/Downloads/grown-workflow/STRUCTURE.md \
       /Users/charliepan/Downloads/grown-workflow/.claude/README.md \
       /Users/charliepan/Downloads/grown-workflow/docs/README.md \
       /Users/charliepan/Downloads/grown-workflow/docs/sdd/README.md \
       /Users/charliepan/Downloads/grown-workflow/docs/superpowers/README.md
```

Expected: 5 个文件均存在。

---

### Task 4: 更新 `.gitignore` 排除 no_git 文件

**Files:**
- Modify: `.gitignore`（末尾追加 no_git 模式）

**Interfaces:**
- Consumes: Task 3 已写好的规范文件
- Produces: 规范文件被 git 忽略，不会出现在 `git status` 中

- [ ] **Step 1: 在 `.gitignore` 末尾追加以下内容**（用 Edit 工具）

````gitignore
# no_git — local-only specification docs (STRUCTURE.md + sub-README)
# These files document project structure & conventions but are intentionally
# not tracked in git. Move them out of this list to commit.
/STRUCTURE.md
/.claude/README.md
/docs/README.md
/docs/sdd/README.md
/docs/superpowers/README.md
````

- [ ] **Step 2: 验证 .gitignore 包含 no_git 段**

```bash
tail -10 /Users/charliepan/Downloads/grown-workflow/.gitignore
```

Expected: 末 10 行包含 `no_git` 注释与 5 个模式。

- [ ] **Step 3: 验证规范文件不被 git 追踪**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git status --short
```

Expected: 输出中**不包含** `STRUCTURE.md`、`.claude/README.md`、`docs/README.md`、`docs/sdd/README.md`、`docs/superpowers/README.md` 任一行。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add .gitignore
git commit -m "chore: gitignore local-only structure spec docs (no_git)"
```

---

### Task 5: CLAUDE.md §6 加 cross-reference

**Files:**
- Modify: `CLAUDE.md`（§6 末尾加一行指引）

**Interfaces:**
- Consumes: Task 3 已写好的 STRUCTURE.md
- Produces: CLAUDE.md §6 末尾指向 STRUCTURE.md，避免内容重复

- [ ] **Step 1: 在 CLAUDE.md §6 末尾追加一行**（用 Edit 工具）

找到 `## §6. 目录约定` 节末尾（在 `**仓库根不放 \`skills/\`、`scripts/\`**`...这一行下面、§7 之前），追加：

````markdown
- **完整结构规范（含目录命名、文件分类、README 要求）见 `STRUCTURE.md`**（本地文件，no_git，不入 git）。
````

- [ ] **Step 2: 验证追加成功**

```bash
grep -A 1 "STRUCTURE.md" /Users/charliepan/Downloads/grown-workflow/CLAUDE.md
```

Expected: 输出包含 `**完整结构规范` 与 `STRUCTURE.md` 引用。

- [ ] **Step 3: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add CLAUDE.md
git commit -m "docs: CLAUDE.md §6 cross-reference to STRUCTURE.md"
```

---

## 附录：规范文件内容

### § A. STRUCTURE.md 内容

写入 `/Users/charliepan/Downloads/grown-workflow/STRUCTURE.md`：

````markdown
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
| `docs/` | 对外文档 + AI 协作过程产物（plans/sdd） | 是 |
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
````

### § B. `.claude/README.md` 内容

````markdown
# `.claude/` 目录说明

> 本目录收纳 Claude Code 项目级配置与 AI 协作产物。
> **no_git**，本地修改即可。

## 内容

| 子项 | 职责 |
|------|------|
| `rules/common/*.md` | 编码规范、测试、安全等通用 rules（与全局 `~/.claude/rules/common/` 同步镜像） |
| `skills/<name>/SKILL.md` | 项目私有 skill，每个 skill 一个目录 |
| `scripts/` | 项目私有脚本（占位） |
| `settings.json` | Claude Code 项目级配置（已启用 ECC 插件） |

## 维护要点

- **新增 skill**：在 `skills/<name>/` 下放 `SKILL.md`，目录名 kebab-case
- **新增 rule**：放到 `rules/common/` 下，单文件单主题（如 `error-handling.md`）
- **不要**在根放 `skills/` 或 `scripts/`——已统一到 `.claude/` 下
````

### § C. `docs/README.md` 内容

````markdown
# `docs/` 目录说明

> 对外文档 + AI 协作过程产物（plans、sdd、superpowers specs）。
> **no_git**，本地修改即可。

## 内容

| 文件/子目录 | 类型 | 说明 |
|-------------|------|------|
| `principles.md` | 文档（commit） | 协作原则 |
| `methodology.md` | 文档（commit） | Skill 沉淀方法论 |
| `plans/` | 过程产物（commit） | 实施性 plan 文档 |
| `sdd/` | 过程产物（commit） | SDD 任务与评审产物 |
| `superpowers/specs/` | 文档（commit） | superpowers 类规格设计 |

## 维护要点

- `plans/` 文件命名：`YYYY-MM-DD-<topic>.md`
- `sdd/` 文件命名：`task-<n>-<brief|report>.md`、`review-<from>..<to>.diff`
- 各子目录有自己的 `README.md`（no_git）说明细节
````

### § D. `docs/sdd/README.md` 内容

````markdown
# `docs/sdd/` 目录说明

> SDD（spec-driven development）过程产物。原位于 `.superpowers/sdd/`，2026-07-11 迁入本目录。
> **commit 入仓**。

## 文件类型

| 类型 | 命名 | 说明 |
|------|------|------|
| 任务简报 | `task-<n>-brief.md` | 每个 SDD 任务的输入 |
| 任务报告 | `task-<n>-report.md` | 每个 SDD 任务的产出 |
| 评审 diff | `review-<from>..<to>.diff` | 两次 commit 之间的代码评审记录 |
| 进度 | `progress.md` | 当前 SDD 流程的进度 |

## 维护要点

- 数字编号按 SDD 流程顺序递增
- `.gitignore` 已在原 `.superpowers/sdd/` 中存在并随迁
````

### § E. `docs/superpowers/README.md` 内容

````markdown
# `docs/superpowers/` 目录说明

> Superpowers 类规格设计文档。
> **commit 入仓**。

## 内容

- `specs/<YYYY-MM-DD>-<topic>-design.md` — superpowers 类设计的规格文档
- 当前含 2 份：claude-md-init、skill-curation-methodology

## 与 `docs/sdd/` 的关系

- `sdd/` — 过程产物（任务、评审、进度）
- `superpowers/specs/` — 设计交付物（规格说明）
- 两者职责不同，**不合并**。详细分工见 `STRUCTURE.md` §3。
````

---

## 验收标准（整体）

执行全部 5 个 task 后，验证：

- [ ] `.superpowers/` 不存在
- [ ] `docs/sdd/` 含原 `.superpowers/sdd/` 所有文件
- [ ] `STRUCTURE.md` 与 4 个子目录 README（`.claude/`、`docs/`、`docs/sdd/`、`docs/superpowers/`）存在
- [ ] `.gitignore` 末尾包含 no_git 段
- [ ] `git status --short` 中**不包含**上述 5 个规范文件
- [ ] CLAUDE.md §6 末尾包含「完整结构规范见 STRUCTURE.md」一行
- [ ] git log 显示 4 个新 commit（不含规范文件）

```bash
# 最终验证
cd /Users/charliepan/Downloads/grown-workflow
echo "=== git log ==="
git log --oneline -5
echo "=== structure ==="
ls -la STRUCTURE.md .claude/README.md docs/README.md docs/sdd/README.md docs/superpowers/README.md
echo "=== .superpowers gone ==="
ls .superpowers 2>&1 | grep -E "No such"
echo "=== docs/sdd exists ==="
ls docs/sdd/ | head -5
echo "=== git status (no_git files must NOT appear) ==="
git status --short
```

预期 5 个新 commit 的 subject：
- `docs: add plan for project structure normalization`
- `docs: revise plan after .superpowers/sdd/ gitignore discovery`
- `refactor: migrate .superpowers/sdd/ to docs/sdd/ (first commit)`
- `chore: gitignore local-only structure spec docs (no_git)`
- `docs: CLAUDE.md §6 cross-reference to STRUCTURE.md`

**不要 push。** push 时机由用户决定。