# Design: grown-workflow 项目 AI 协作契约初始化

**Date:** 2026-07-10
**Status:** Draft — awaiting user review
**Topic:** 为 grown-workflow 仓库建立 AI 协作基础设施（CLAUDE.md、plans/、skills/、scripts/、ECC 命令清单、git 频率规范）

---

## 1. 背景与目标

`grown-workflow` 是一个 AI 协作方法论套件（v0 阶段）。README 谈「为什么」，本设计谈「怎么做」。

当前仓库已有：
- `README.md`（方法论主文档）
- `docs/principles.md`（哲学原理姊妹篇）
- `CONTRIBUTING.md`（v0 节奏说明）
- `.claude/settings.json`（ECC 插件已启用）
- `.claude/rules/common/`（通用编码规范 10 个 .md）
- 仓库根 `skills/`、`scripts/`（仅 `.gitkeep`）
- 仅 2 个 commit

**目标：** 为本仓库建立 AI 协作基础设施，使 Claude Code 在本项目内工作时有一份明确的本地契约可循。

## 2. 范围

### 2.1 做

- 新增仓库根 `CLAUDE.md`（主 AI 协作契约）
- 新增 `docs/plans/` 文件夹及 README 模板
- 新增 `.claude/skills/` 与 `.claude/scripts/`（各含 `.gitkeep`）
- 删除仓库根 `skills/`、`scripts/`（已统一到 `.claude/` 下）
- 修改 `README.md` 增加指向 CLAUDE.md 的引用
- 修改 `CONTRIBUTING.md` 补充 git push 流程细则

### 2.2 不做

- 不实际编写任何 skill 代码（仅建脚手架）
- 不修改 `.claude/rules/common/` 内容
- 不修改 `.claude/settings.json`（ECC 插件已正确启用）
- 不 push 到远端（push 由用户决定时机）

## 3. 目录结构

```
/Users/charliepan/Downloads/grown-workflow/
├── CLAUDE.md                   # 新增 - 主 AI 协作契约
├── README.md                   # 修改 - 末尾加 CLAUDE.md 引用
├── CONTRIBUTING.md             # 修改 - 加 push 流程
├── docs/
│   ├── principles.md           # 现有
│   ├── plans/                  # 新增
│   │   ├── README.md           # 新增 - plan 工作流说明
│   │   └── .gitkeep
│   └── superpowers/            # 新增（本设计文档位置）
│       └── specs/
│           └── 2026-07-10-claude-md-init-design.md
├── .claude/
│   ├── settings.json           # 现有 - 不动
│   ├── rules/
│   │   └── common/             # 现有 - 不动
│   ├── skills/                 # 新增 (迁移自根 skills/)
│   │   └── .gitkeep
│   └── scripts/                # 新增 (迁移自根 scripts/)
│       └── .gitkeep
├── skills/                     # 移除
└── scripts/                    # 移除
```

## 4. CLAUDE.md 内容设计

CLAUDE.md 总长约 300-400 行，分为 8 节：

### §0. 决策原则（最高优先级）

```
- 任何不清楚、模糊、不确定、不知道选哪个 → 直接用 AskUserQuestion 问，不要替我做决策
- 复杂任务（跨多文件 / 多阶段 / 跨多日）→ 先写 plan，再实施
- 拍板权不可委托：让 AI 替你定方向是反模式
```

### §1. Git 提交频率规范

```
- 本地提交：高频、一次一个意图（沿用 CONTRIBUTING.md）
- Push 前：必须先 rebase/squash 合并，整理 commit 历史
- 合并粒度：每个 push 的 commit 列表应是一个连贯的「意图批次」
```

### §2. ECC 命令速查

本项目强制使用 ECC 插件（已在 `.claude/settings.json` 启用 `ecc@ecc`）。常用 8 个命令：

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

### §3. Plans 工作流

- **触发条件：** 多文件 / 多阶段 / 跨多日 / 含架构决策 / 涉及不熟悉库
- **位置：** `docs/plans/YYYY-MM-DD-<topic>.md`
- **流程：** AskUserQuestion 确认范围 → 写 plan → 实施中持续更新 → 完成时回顾
- **原则：** plan 是活记录，不是出发前的门票

### §4. DO（应该做的）— 13 条

分组：决策、流程、信息获取、代码质量、错误处理、安全

1. 用 AskUserQuestion 澄清
2. 复杂任务先写 plan
3. 本地提交高频、一次一个意图
4. push 前先合并
5. 用 ECC 命令
6. 库文档查 Context7
7. 并行任务用并行 Agent
8. 改动完成请求 code-review
9. 测试驱动
10. 错误显式处理
11. 不可变数据
12. 输入边界验证
13. Secrets 走环境变量

### §5. DON'T（不要做的）— 17 条，分 7 组

- **决策类（2）：** 不要替我拍板；不要假设需求
- **流程类（4）：** 不要跳过 plan；不要混合意图 commit；不要未经合并直接 push；不要跳过 code-review
- **信息获取类（2）：** 不要用 WebSearch 查库文档；不要凭记忆写库 API
- **代码质量类（5）：** 不要长函数（>50 行）；不要超大文件（>800 行）；不要深度嵌套（>4 层）；不要 mutation；不要硬编码 secrets
- **错误与可观测性（2）：** 不要默默吞错误；不要留 console.log
- **测试（1）：** 不要跳过测试
- **提交安全（1）：** 不要提交敏感数据

### §6. 目录约定

```
- .claude/ — Claude Code 配置 + AI 协作产物（plans、skills、scripts、rules）
- docs/ — 对外文档（principles、plans）
- 仓库根不放 skills/、scripts/（已统一到 .claude/ 下）
```

### §7. 与现有 rules 的关系

本文件补充 `~/.claude/rules/` 全局规则之上，不替代。`.claude/rules/common/` 内是通用编码规范补充。

## 5. Plans 文件夹工作流

`docs/plans/README.md` 内容：

```markdown
# Plans

复杂任务的 plan 文档存放处。Plan 是活记录,不是出发前的门票。

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
```

## 6. 提交策略

按 git 频率规则，本次初始化拆为 6 个本地 commit（不 push）：

```
1. chore: add .claude/skills/ and .claude/scripts/ scaffolds
2. chore: remove root skills/ and scripts/ (consolidated into .claude/)
3. docs: add docs/plans/ with README template
4. docs: add CLAUDE.md (AI collaboration contract)
5. docs: link README.md to CLAUDE.md
6. docs: detail git push normalization in CONTRIBUTING.md
```

每个 commit 一个意图；commit 1、2 是脚手架迁移；3、4、5、6 是文档。

## 7. 风险与权衡

| 风险 | 缓解 |
|------|------|
| CLAUDE.md 后续膨胀到难以维护 | 监控行数，超过 ~500 行考虑拆分到 `.claude/rules/` |
| 删除根 `skills/`、`scripts/` 与 README 描述的「分享 skill」目的冲突 | 用户的明确选择；本设计遵循。如未来需要重新引入根目录版本，可走规范化 commit |
| ECC 命令清单与 ECC 官方更新脱节 | 列在 CLAUDE.md 的命令是最常用的 8 个；用户被引导自行查阅官方文档以了解完整命令 |
| 本设计文档不在 `docs/plans/` 下 | 设计文档遵循 brainstorming skill 默认路径 `docs/superpowers/specs/`；`docs/plans/` 专用于实施性 plan |

## 8. 验收标准

- [ ] 仓库根存在 `CLAUDE.md`，含 §0-§7 全部节
- [ ] `docs/plans/README.md` 存在且含模板
- [ ] `.claude/skills/`、`.claude/scripts/` 存在（各含 `.gitkeep`）
- [ ] 仓库根 `skills/`、`scripts/` 已删除
- [ ] `README.md` 末尾引用了 CLAUDE.md
- [ ] `CONTRIBUTING.md` 含 push 流程细则
- [ ] 6 个本地 commit 已完成（不 push）
- [ ] 本设计文档已提交到 git
