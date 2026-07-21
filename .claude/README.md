# 关于本项目 / About This Project

---

## 项目本质 / Project Essence

**grown-workflow** 不是一个生产软件产品的项目。它是一个 **元项目（meta-project）**——一套关于"如何结构化 AI 协作"的方法论与工具箱，并且它本身就是自身方法的活体示范。

**grown-workflow** is not a project that produces software. It is a **meta-project** — a methodology and tooling kit for *how to structure AI-augmented collaboration* — and it is itself a living demonstration of its own principles.

核心观察（Core insight）：这个项目不是先画图纸再施工的。它的方法论是从一百多次提交的实践中自己"长出来"的，而这份经历本身被记录成了 `README.md` 里的文章。项目文档与项目实践互为表里。

> This project was not designed upfront and then built. Its methodology *grew* from 100+ commits of real practice, and that journey was distilled into the essay in `README.md`. The project's documentation and its practice reflect each other.

---

## 三个核心母题 / Three Core Themes

项目方法论围绕三条从实践中观察到的路径展开（详见 `README.md`）：

The methodology revolves around three paths observed from practice (see `README.md` for the full essay):

### 一、脚手架先于项目 / Scaffolding Before Project

AI 协作契约（即 `CLAUDE.md`）要在项目早期就建立，从 **v0** 开始，承认它会被不断重写。命名要前向兼容，迁移路径要预留。规则一旦写定就会产生迁移成本——所以第一版必须是 v0，不是 v1。

Write the AI collaboration contract (`CLAUDE.md`) early as **v0**, acknowledging it will be rewritten. Naming must be forward-compatible; migration paths must be预留的. The first version must be v0, not v1 — once a rule is set, changing it incurs migration costs.

### 二、推进与规范化交替 / Progress Alternates with Normalization

工作不是单向推进的。节奏是"推进一段→停下来规范化→再推进"。规范化的不是"顺手打扫卫生"，而是显式阶段——扫描结构漂移、修复命名不一致、整理 tag。要为它争取和推进同等的时间预算与可见度。

Work does not move forward in one direction. The rhythm is: *advance → pause to normalize → advance again*. Normalization is not "tidying up along the way" — it is an explicit phase for scanning structural drift, fixing naming inconsistencies, and整理 tags. It deserves equal time budget and visibility as feature work.

### 三、工具从痛点长出来 / Tools Grow from Pain Points

不要预先架构工具。工具的生命力来自它解决过一次真实的、重复的痛。**3 次重复信号**：一个工作步骤在不同情境下被重复 3 次以上时，才把它沉成工具。工具追着痛点长，痛点追着情境冒。

Do not pre-architect tools. A tool's vitality comes from having solved a real, repeated pain. **The 3-repetition signal**: only formalize a step into a tool after it has been repeated 3+ times in different contexts. Tools chase pain; pain chases context.

---

## 产出层文件概览 / Output Layer Overview

| 层面 / Layer | 文件 / File | 作用 / Purpose |
|-------------|-------------|---------------|
| **哲学原理** / Philosophy | `docs/principles.md` | 委托边界、计划的本质、可见即信任 / Delegation boundaries, the nature of plans, visibility as trust |
| **实践方法论** / Practice | `README.md` | 三件主题的操作化叙述 / Operationalized narrative of the three themes |
| **Skill 沉淀流程** / Skill Curation | `docs/methodology.md` | 4 阶段流程：接收→疼痛溯源→沉淀→跑一次 / 4-stage process: receive → trace pain → formalize → run once |
| **具体工作流** / Workflow | `.claude/skills/ecc-workflow/SKILL.md` | 8 个精选 ECC 命令的编排与本地约定 / 8 curated ECC commands with local conventions |
| **协作契约** / Contract | `CLAUDE.md` | 项目的 AI 行为规则与 DO/DON'T / AI behavior rules and DO/DON'T |

---

## 文件自洽性 / Self-Consistency

项目文档之间高度自洽，方法论的原则在其自身结构中得到了体现：

The project's documentation is highly self-consistent — the methodology's principles are reflected in its own structure:

| 原则 / Principle | 实例 / Evidence |
|-----------------|----------------|
| 工具从痛点长出来 / Tools grow from pain | `docs/methodology.md` Stage 2 强制问"重复了几次"，3 次信号才沉淀 |
| 工具替代判断处停下 / Stop at judgment | `docs/methodology.md` Stage 2 问题 3 强制分流：选 B（全是判断）时停下 |
| v0 正确姿态 / v0 posture | 跑一次后必须写"v0 已知不足"段；不写就是没沉淀完 |
| 推进与规范化交替 / Alternate phases | `CLAUDE.md` 有明确的 DO/DON'T 和 AskUserQuestion 触发场景表 |
| 拍板权不可委托 / Decisions not delegated | `docs/principles.md` → `CLAUDE.md` "不确定→问"原则直接对应 |
| 脚手架先于起步 / Scaffold before start | `CLAUDE.md` 在仓库第 6 次提交时已出现，至今仍在改写 |

---

## 附录：`.claude/` 目录说明 / Appendix: `.claude/` Directory Guide

| 子项 / Item | 职责 / Responsibility |
|-------------|----------------------|
| `rules/common/*.md` | 编码规范、测试、安全等通用 rules（与全局 `~/.claude/rules/common/` 同步镜像） / Coding standards, testing, security (mirrored from global `~/.claude/rules/common/`) |
| `skills/<name>/SKILL.md` | 项目私有 skill，每个 skill 一个目录 / Project-local skills, one directory per skill |
| `scripts/` | 项目私有脚本（占位） / Project-local scripts (placeholder) |
| `settings.json` | Claude Code 项目级配置 / Claude Code project-level configuration |

### 维护要点 / Maintenance Notes

- **新增 skill**：在 `skills/<name>/` 下放 `SKILL.md`，目录名 kebab-case
- **新增 rule**：放到 `rules/common/` 下，单文件单主题（如 `error-handling.md`）
- **Add a skill**: place `SKILL.md` under `skills/<name>/`, directory name in kebab-case
- **Add a rule**: place in `rules/common/`, one topic per file
