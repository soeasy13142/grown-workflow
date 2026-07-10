# Design: Skill 整理方法论 v0

**Date:** 2026-07-10
**Status:** Draft — awaiting user review
**Topic:** 为 grown-workflow 设计「用户给我 skill，我怎么整理」的方法论，作为 v0 沉淀到 docs/methodology.md（独立 markdown）。

---

## 1. 背景与目标

`grown-workflow` 是一个 AI 协作方法论套件。README 谈「为什么」，本设计谈「怎么做 skill 整理」。

README 的三件主题：
1. 脚手架先于项目（已完成 v0：CLAUDE.md、docs/plans/、.claude/skills/ 收纳）
2. 推进与规范化交替
3. 工具从痛点长出来

README 还给出了：
- 3 次重复信号（一个工作步骤被重复 3+ 次才沉成工具）
- 工具替代判断处停下（判断归人，收集归工具）
- 过早抽象 vs 拒绝抽象（两个都常见；信号是"用户开始觉得烦"）
- v0 正确姿态（先写可用的，显式记下已知不足）

**本方法论要解决：** 用户给一个 skill 给我（任意形态），我怎么把它整理成可分享的、v0 状态的、放在 `.claude/skills/<name>/` 下的 SKILL.md。

**目标：** 一份 v0 简单可用的方法论，不预设 schema、不引入状态机、不抢用户的判断权。

## 2. 范围

### 2.1 做

- 设计 4 阶段流程：接收 → 疼痛溯源 → 沉淀 → 跑一次
- 定义每个阶段的输入、动作、产出
- 给出 SKILL.md 的 v0 自由模板
- 列出避坑（6 个反模式）
- 给出升级到方案 B 的触发条件
- 沉淀到 `docs/methodology.md`（独立 markdown，与 CLAUDE.md 分开）
- 给一个示范用法（用户给我 skill「PDF 抽图嵌入章节」）

### 2.2 不做

- 不预设 skill 状态机（seed → draft → curated → verified → deprecated）
- 不强制 SKILL.md 的 schema（v0 自由）
- 不写测试除非用户明确要 TDD
- 不替用户做命名（在 Stage 3 用 AskUserQuestion 问）
- 不写工具自动跑 Stage 4（v0 靠我自己保证）
- 不引入 skill 互引机制、skill 弃用流程（升级到方案 B 时再做）

## 3. 方法论：4 阶段流程

### Stage 1: 接收

**输入：** 用户给的任意形态 skill——一句话、脚本、描述、workflow、想法。

**动作：** 原样接住，不要求结构化。

**产出：** raw seed（对话里，或暂存在 `.superpowers/skill-curation/<name>-raw.md`）

**不做：**
- 不要求用户结构化
- 不立刻写 SKILL.md
- 不替用户做命名

### Stage 2: 疼痛溯源

**输入：** Stage 1 的 raw seed。

**动作：** 用 3 个 AskUserQuestion 问清三件事。

**问题 1 — 痛点本体：**
> 这个 skill 是为了解决什么重复的痛？请用一两句话描述「什么动作在什么情境下被重复」。

**问题 2 — 重复次数：**
> 这个问题在历史上被重复过几次？3 次以下通常说明还不是 skill，是一次性 case。

**问题 3 — 判断/收集边界：**
> 这个 skill 替代的是「资料收集」还是「判断」？
> - A. 资料收集（重复的是机械动作，让 skill 做）
> - B. 判断（重复的是决策，**必须留给人**）
> - C. 两者都有（请描述哪部分归 skill、哪部分留给人）

**关键：** 如果问题 3 选 B，停下来跟用户讨论「这个不该做成 skill」。

**产出：** 痛点笔记（写到 `.superpowers/skill-curation/<name>-pain.md`）

### Stage 3: 沉淀为 SKILL.md

**触发条件：** Stage 2 的 3 个问题都答完，且问题 3 不全是 B。

**动作：**
1. 命名：用 AskUserQuestion 问，3-4 个候选名
2. 创建 `.claude/skills/<name>/` 目录
3. 写 SKILL.md（见 §4 模板）
4. 可选：放 scripts/、examples/、tests/（v0 不必）

**不做：**
- 不写测试除非用户明确说
- 不写 frontmatter schema 强迫所有 skill 套用同一格式

**产出：** `.claude/skills/<name>/SKILL.md`（可能含 scripts/、examples/、tests/）

### Stage 4: 跑一次

**输入：** Stage 3 的 SKILL.md。

**动作：**
- 找一个真实场景跑这个 skill
- 把跑出来的结果、踩到的坑、未覆盖的边界，写到 SKILL.md 末尾的「v0 已知不足」段
- 这一段 v0 必备，**不可省略**

**不做：**
- 不为了"看起来完整"而虚构跑过的结果
- 不省略"已知不足"段

**产出：** SKILL.md 末尾追加「v0 已知不足」段（v0 沉淀完成）

## 4. SKILL.md 模板（v0 自由）

不强制 schema。最小可用骨架：

```markdown
---
name: <skill-name>
description: <一句话：做什么、何时用>
status: v0  # 或 deprecated
---

# <Skill Name>

## 是什么
<一段：解决什么痛点>

## 什么时候用
<3-5 个 trigger 描述>

## 步骤
<1-N 步，可以是 prompt、shell 命令、文件操作>

## 已知不足（v0）
<跑一次后填的：踩到的坑、未覆盖边界、待优化>

## 历史
- YYYY-MM-DD: v0 沉淀（来自用户描述「<原始一句话>」）
```

**v0 自由：** 字段都可选。复杂 skill 加 `## 示例`、`## 失败模式`；简单 skill 只填 4 段也行。

**前向兼容：** `name`、`description` 必填（Claude Code 加载需要）；其他字段是文档骨架，不绑死。

## 5. 避坑（来自 README 母题）

| 反模式 | 为什么错 | 正确做法 |
|--------|----------|----------|
| **为 3 个 skill 设计统一 schema** | 过早抽象 | v0 自由，重复 3+ 次再抽象 |
| **SKILL.md 没跑过就 commit** | 违反「跑一次才算数」 | Stage 4 必跑 |
| **省略「v0 已知不足」段** | 违反 v0 显式姿态 | 跑一次后必须补这一段 |
| **skill 替用户做判断** | 违反「工具替代判断处停下」 | Stage 2 问题 3 必须分流 |
| **写完美 frontmatter** | 违反 v0 心态 | 留下"已知不足"清单即可 |
| **混同"打扫卫生"和"规范化"** | 违反 README 二、第三节 | 规范化是显式阶段，独立计时 |

## 6. 何时升级到方案 B

**触发条件（满足任一）：**
- `.claude/skills/` 下的 skill 数量 ≥ 5
- 出现 SKILL.md 之间结构漂移（同一个信息字段命名不一致）
- 「v0 已知不足」段出现重复模式（说明规范化时机到了）
- 出现「让我做 X skill」被同义反复提了 3+ 次

**升级动作：**
- 加 Stage 5：规范化扫（周期性对所有 .claude/skills/ 做结构漂移扫描）
- 加 Stage 6：v0 → v1 升级路径
- 仍不引入状态机（除非 skill 数量 ≥ 20）

## 7. 与本项目其他规范的关系

- **CLAUDE.md §0 决策原则：** Stage 2 的 3 个问题正是这条原则的实例化
- **CLAUDE.md §3 plans 工作流：** 复杂 skill 沉淀需要 plan（跨多文件 / 涉及现有 skills 互引时）
- **CONTRIBUTING.md git 节奏：** SKILL.md 沉淀按"一次一个意图"提交

## 8. 示范用法（未来）

用户：「我每次写一篇长笔记都要手动补 callout、mermaid、aliases、Dataview 查询，这个能不能做成 skill？」

按本方法论：
1. Stage 1: 接收——一句话 seed「给长笔记补 callout、mermaid、aliases、Dataview 查询」
2. Stage 2: 3 个问题
   - 痛点：长笔记的元数据补充是重复动作
   - 重复次数：「这篇是第 14 次了」→ 通过 3 次信号
   - 边界：callout/mermaid/aliases/Dataview 都是模板化的（资料收集）→ A
3. Stage 3: 命名候选 `vault-enhance`（README 提到的现成名字），写 SKILL.md
4. Stage 4: 在一篇真实长笔记上跑一次，记下「已知不足」

## 9. 风险与权衡

| 风险 | 缓解 |
|------|------|
| 3 个问题漏掉复杂场景 | v0 已知不足段显式记下，升级到 B 时补 |
| Stage 4 「跑一次」靠我自己保证 | 方法论自身的已知不足段记录 |
| 没有 skill 互引、弃用机制 | 升级到方案 B 时引入 |
| 用户用形态超出预期（视频、对话） | v0 显式说明方法论 v0 适用范围 |

## 10. 验收标准

- [ ] `docs/methodology.md` 存在并含 4 阶段流程
- [ ] `docs/methodology.md` 末尾含「v0 已知不足」段（方法论自身的）
- [ ] 含 6 个反模式表
- [ ] 含 4 个升级触发条件
- [ ] 与 README 母题映射清晰
- [ ] 设计文档已提交到 git

## 11. v0 已知不足（方法论自身的）

诚实记录方法论 v0 的不足：
- 3 个问题不覆盖所有形态（极复杂 skill 可能漏）
- 「跑一次」没有自动化，靠我自己保证
- 没有"skill 互引"机制
- 没有"skill 弃用"流程（只有 status 字段）
- 命名约定是自由发挥的（升级到方案 B 时再规范）
