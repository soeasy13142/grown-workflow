# grown-workflow

[![GitHub](https://img.shields.io/badge/GitHub-soeasy13142/grown--workflow-181717?logo=github)](https://github.com/soeasy13142/grown-workflow)
[![License](https://img.shields.io/github/license/soeasy13142/grown-workflow?color=blue)](LICENSE)

[**简体中文**](.claude/README.md) | [English](.claude/README.en.md)

> **让 AI 协作先有脚手架、规范穿插于推进、工具从痛点长出来。**

---

## 关于本项目

grown-workflow 不是一个生产软件产品的项目。它是一个 **元项目（meta-project）**——一套关于"如何结构化 AI 协作"的方法论与工具箱，并且它本身就是自身方法的活体示范。

项目的方法论不是先画图纸再施工的，而是从一百多次提交的实践中自己"长出来"的。这段经历被记录成了 [`README.md`](../README.md) 里的文章，而本仓库的结构本身也是这套方法的实证。

### 三个核心母题

| 母题 | 一句话概括 |
|------|-----------|
| **脚手架先于项目** | AI 协作契约（CLAUDE.md）从 v0 开始，承认它会被不断重写 |
| **推进与规范化交替** | 推一段→停一下规范化→再推进；规范化是显式阶段 |
| **工具从痛点长出来** | 3 次重复信号才沉成工具，工具追着痛点长 |

详见 [`README.md`](../README.md) 全文。哲学原理见 [`docs/principles.md`](../docs/principles.md)。

---

## Skills

本项目沉淀的 skill 位于 `.claude/skills/<name>/` 目录下，每个 skill 含 SKILL.md 核心文档及附属资料。

### ecc-workflow — ECC 精选工作流

**用途** — 封装 [ECC（Enhanced Claude Capabilities）](https://github.com/affaan-m/ECC) 的 8 个精选命令，附带项目本地约定与编排指南。

**用法** — 按需从场景速查表选取起点命令，可串联为一个完整工作流：

| 命令 | 用途 |
|------|------|
| `/ecc:plan` | 功能规划与任务拆解 |
| `/tdd` | 测试驱动开发 |
| `/ecc:code-review` | 代码质量审查 |
| `/ecc:build-fix` | 修复构建错误 |
| `/ecc:refactor-clean` | 死代码清理 |
| `/e2e` | 端到端测试 |
| `/ecc:test-coverage` | 覆盖率分析 |
| `/ecc:update-docs` | 文档更新 |

**链接** — [ECC 官方仓库](https://github.com/affaan-m/ECC) · [skill 文档](skills/ecc-workflow/SKILL.md)

---

### obsidian-vault-enhance — Obsidian 笔记增强

**用途** — 自动为 Obsidian 笔记补充 Dataview 查询、Mermaid 图表、语义化 Callout、别名、Templater 模板等高级功能。根据笔记所在目录和文件名自动识别类型（HCIP / HCIA / RHEL / Index / Python / General），按类型应用不同套件。

**用法** — 在 Claude Code 中触发后按流程执行：

```
Phase 1: 读取笔记 → 识别类型（按文件夹 + 文件名前缀）
Phase 2: 理解内容 → 判定可用的增强类型（是否有流程可画图、是否有命令可示例）
Phase 3: 通用增强（frontmatter + 别名 + fileClass 验证）
Phase 4: 类型特定增强（摘要 callout / 考点 / Mermaid 拓扑 / Dataview 索引）
Phase 5: 验证（frontmatter 完整性 + callout + 断链检查）
```

**链接** — [skill 文档](skills/obsidian-vault-enhance/SKILL.md) · [Mermaid 模板参考](skills/obsidian-vault-enhance/references/mermaid-templates.md) · [Dataview 查询参考](skills/obsidian-vault-enhance/references/dataview-queries.md)

---

## 仓库内容

```
grown-workflow/
|
|-- README.md               # 方法论文章（三个核心母题）
|-- CLAUDE.md               # AI 协作主契约（项目级行为规范）
|-- CONTRIBUTING.md         # 贡献指南与 Git 操作规范
|-- CREDITS.md              # 第三方致谢与许可证
|-- LICENSE                 # MIT 许可证
|-- STRUCTURE.md            # 仓库结构说明（已归档）
|
|-- .claude/
|   |-- README.md           # 项目说明（本文档）
|   |-- README.en.md        # Project description (English)
|   |-- settings.json       # Claude Code 项目配置
|   |-- skills/
|   |   |-- ecc-workflow/           # ECC 精选工作流
|   |   |   |-- SKILL.md            #   核心文档
|   |   |   |-- commands/           #   8 个命令详解
|   |   |       |-- ecc-plan.md
|   |   |       |-- tdd.md
|   |   |       |-- ecc-code-review.md
|   |   |       |-- ecc-build-fix.md
|   |   |       |-- ecc-refactor-clean.md
|   |   |       |-- e2e.md
|   |   |       |-- ecc-test-coverage.md
|   |   |       |-- ecc-update-docs.md
|   |   |-- obsidian-vault-enhance/  # Obsidian 笔记增强
|   |       |-- SKILL.md             #   核心文档
|   |       |-- references/
|   |           |-- mermaid-templates.md # Mermaid 图模板参考
|   |           |-- dataview-queries.md  # Dataview 查询参考
|   |-- rules/
|   |   |-- common/               # 通用编码规范（与全局同步）
|   |       |-- coding-style.md
|   |       |-- testing.md
|   |       |-- git-workflow.md
|   |       |-- code-review.md
|   |       |-- security.md
|   |       |-- performance.md
|   |       |-- patterns.md
|   |       |-- hooks.md
|   |       |-- agents.md
|   |       |-- development-workflow.md
|   |-- scripts/                   # 项目脚本（占位）
|
|-- docs/
    |-- README.md              # docs/ 目录说明（已归档）
    |-- principles.md          # 哲学原理
    |-- methodology.md         # Skill 整理方法论
    |-- plans/
    |   |-- README.md          # plans/ 目录说明
    |   |-- ...plan.md         # 规划记录
    |-- sdd/
    |   |-- README.md          # sdd/ 目录说明
    |   |-- ...                # SDD 过程记录
    |-- superpowers/
        |-- README.md          # superpowers/ 目录说明
```

---

## 如何开始

```bash
# 确认 ECC 插件已启用（`.claude/settings.json` 中配置）
cat .claude/settings.json

# 不确定从哪个命令开始？看场景速查表：
cat .claude/skills/ecc-workflow/SKILL.md | grep "| 你的场景" -A 20

# 浏览 CLAUDE.md 了解项目协约
cat CLAUDE.md
```

---

> 本项目遵循"脚手架先于起步、推进与规范化交替、工具从痛点长出来"的演化路径。详见 [`README.md`](../README.md)。
