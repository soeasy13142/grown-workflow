# grown-workflow

AI 协作契约——本文件是仓库的主契约，Claude Code 自动加载。
详见 [README.md](README.md) 方法论总纲。

- **语言**: Markdown, Bash
- **核心技术**: CLAUDE.md 契约、ECC 工作流、Skills 方法论

## Quick Start

```bash
# 查看项目方法论（建议优先阅读）
cat README.md
cat docs/principles.md

# ECC 工作流入口 — 在 Claude Code 中使用斜杠命令
# /ecc:plan /tdd /ecc:code-review /ecc:build-fix
# /ecc:refactor-clean /e2e /ecc:test-coverage /ecc:update-docs
# 详见 .claude/skills/ecc-workflow/ 下的各命令文档
```

## Key Conventions

- **不确定→问**：遇到方向/选型/命名/阈值模糊时先 AskUserQuestion，不替用户拍板。详见 §0 场景表
- **本地提交高频、一次一个意图**：一个小改动一个 commit，不混多个意图
- **Push 前整理**：`git rebase -i`，把本地细粒度 commit 整理成「意图批次」
- **复杂任务先写 plan**：多文件/多阶段/跨多日/含架构决策时，先在 `docs/plans/` 写 plan
- **ECC 命令优先**：§2 列出的命令是本项目首选入口，不用手工拼凑等价流程
- **库文档查 Context7**：涉及具体库/框架/API 时用 Context7 MCP，不走 WebSearch
- **不可变数据**：update 不 mutate，改写时返回新对象
- **错误显式处理**：不 swallow errors；UI 层友好消息，服务层记详细上下文
- **输入边界验证**：系统边界处用 schema 验证，失败快速失败
- **Secrets 走环境变量**：不硬编码；启动时校验必需 env 已存在
- **测试驱动**：新功能走 `/tdd`，先写测试再写实现
- **改动完成请求 code-review**：走 `/ecc:code-review` 或 `code-reviewer` Agent

### AskUserQuestion 触发场景

以下场景任意命中即触发 AskUserQuestion，不要替用户判断「够清楚了」：

| # | 场景 | 典型模糊输入 | 应问什么 |
|---|------|-------------|---------|
| 1 | 模糊动词/形容词 |「优化下」「重构一下」 | 目标？指标？范围？ |
| 2 | 选型决策 |「用啥库」 | 列 ≥2 候选 + 推荐，用户挑 |
| 3 | 阈值与边界 |「长函数」「大文件」 | 具体数字选项 |
| 4 | 命名/标识符 |「函数叫啥」 | 给 ≥2 候选，用户定 |
| 5 | 范围与粒度 |「改一下」 | 一行/单文件/模块/全仓库？ |
| 6 | 风格与偏好 |「按你想法」 | 错误处理/注释风格等 |
| 7 | 优先级/顺序 | 多任务堆在一起 | 先做哪个？并行？ |
| 8 | 默认值 | 超时/重试/缓存 | 用 A 还是 B？ |

## Module Boundaries

| 目录 | 职责 | 禁止 |
|------|------|------|
| `.claude/skills/` | 沉淀的 skill 成果物 | 不引用外部未沉淀的 skill |
| `.claude/rules/` | 工作流与编码规范 | 不替代 CLAUDE.md 主契约角色 |
| `docs/plans/` | plan 工作流的过程记录 | 不可做核心产出引用 |
| `docs/sdd/` | SDD 方法论的过程记录 | 不可做核心产出引用 |
| `docs/`（principles/methodology） | 对外分享的方法论文档 | — |

## DO / DON'T

### ✅ DO
- DO 用 AskUserQuestion 澄清模糊需求（见触发场景表）
- DO 复杂任务先写 plan 再动手
- DO 本地提交高频、一次一个意图
- DO push 前先 rebase/squash 合并
- DO ECC 命令作为首选入口
- DO 用 Context7 查库文档
- DO 并行任务用并行 Agent
- DO 动作完成请求 code-review
- DO 测试驱动（先 RED 再 GREEN）
- DO 错误显式处理、输入边界验证、不可变数据

### ❌ DON'T
- DON'T 替用户拍板 — 方向/命名/选型必须 AskUserQuestion
- DON'T 假设需求 — 含糊的先确认，不要「我以为」
- DON'T 跳过 plan — 满足触发条件时直接动手是反模式
- DON'T 混合意图 commit、未经合并直接 push
- DON'T 跳过 code-review
- DON'T 凭记忆写库 API — 走 Context7 验证
- DON'T 写 >50 行函数、>800 行文件、>4 层嵌套
- DON'T 用 mutation 模式 — 改写返回新对象
- DON'T 硬编码 secrets、默默吞错误、留 console.log/debug 痕迹
- DON'T 跳过测试

## Architecture

```
grown-workflow/
├── CLAUDE.md        ← 主契约（本文件）
├── README.md        ← 项目概述与方法论
├── CONTRIBUTING.md  ← 开发者指南
├── CREDITS.md       ← 第三方致谢
│
├── .claude/
│   ├── skills/      ← skill 成果物
│   ├── rules/       ← 工作流规范
│   └── settings.json ← Claude Code 配置
│
└── docs/
    ├── plans/       ← 规划记录（副产品）
    ├── sdd/         ← SDD 记录（副产品）
    ├── principles.md ← 对外方法论
    └── methodology.md ← 对外方法论
```

核心原则：脚手架先于起步 / 推进与规范化交替 / 工具从痛点长出来。

## Reference

| 文档 | 用途 |
|------|------|
| [README.md](README.md) | 项目概述与方法论总纲 |
| [CONTRIBUTING.md](CONTRIBUTING.md) | 开发者指南与 Git 规范 |
| [CREDITS.md](CREDITS.md) | ECC 第三方致谢与许可证 |
| [docs/principles.md](docs/principles.md) | 核心原则：委托、规划与可见性 |
| [docs/methodology.md](docs/methodology.md) | Skill 整理方法论（4 阶段流程） |
| `.claude/skills/ecc-workflow/SKILL.md` | ECC 工作流总览 |
| `.claude/skills/ecc-workflow/commands/` | ECC 各命令详细用法 |
| [.claude/rules/common/](.claude/rules/common/) | 通用编码规范（complement 全局 rules） |
