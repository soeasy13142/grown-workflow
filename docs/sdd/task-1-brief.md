### Task 1: 新增 `docs/methodology.md`（Skill 整理方法论 v0）

**Files:**
- Create: `docs/methodology.md`

**Interfaces:**
- Consumes: nothing
- Produces: 单文件方法论文档，6 个节（导言 + 4 阶段 + 模板 + 反模式 + 升级 + 已知不足）

- [ ] **Step 1: 创建 `docs/methodology.md`，完整内容如下**

写入文件 `/Users/charliepan/Downloads/grown-workflow/docs/methodology.md`，内容为：

````markdown
# Skill 整理方法论（v0）

> 本仓库收录 skill 的方法。一句话：**接收任意形态 → 疼痛溯源 → 沉淀为 SKILL.md → 跑一次，记下不足。**
>
> v0 自由格式，不预设 schema，不引入状态机。本方法论自身也带 v0 已知不足段（见末尾）。

## §0. 与 README 母题的对应

本方法论严格对齐 `README.md` 的三件主题：

| README 母题 | 本方法论对应 |
|------------|-------------|
| 工具从痛点长出来 | Stage 2 强制问"重复了几次"，3 次信号才沉淀 |
| 工具替代判断处停下 | Stage 2 问题 3 强制分流：选 B（全是判断）时停下 |
| v0 正确姿态 | 跑一次后必须写「v0 已知不足」段；不写就是没沉淀完 |
| 推进与规范化交替 | 规范化是显式阶段（见 §5 升级触发条件） |
| 过早抽象是反模式 | 不为 3 个 skill 设计统一 schema |

## §1. Stage 1 — 接收

**输入：** 用户给的任意形态 skill——一句话、脚本、描述、workflow、想法。

**动作：** 原样接住，不要求结构化。

**产出：** raw seed（对话里，或暂存在 `.superpowers/skill-curation/<name>-raw.md`）

**不做：**
- 不要求用户结构化
- 不立刻写 SKILL.md
- 不替用户做命名（要等 Stage 3 问）

## §2. Stage 2 — 疼痛溯源（关键阶段）

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

## §3. Stage 3 — 沉淀为 SKILL.md

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

## §4. Stage 4 — 跑一次

**输入：** Stage 3 的 SKILL.md。

**动作：**
- 找一个真实场景跑这个 skill
- 把跑出来的结果、踩到的坑、未覆盖的边界，写到 SKILL.md 末尾的「v0 已知不足」段
- 这一段 v0 必备，**不可省略**

**不做：**
- 不为了"看起来完整"而虚构跑过的结果
- 不省略"已知不足"段

**产出：** SKILL.md 末尾追加「v0 已知不足」段（v0 沉淀完成）

## §5. SKILL.md 模板（v0 自由）

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

## §6. 避坑（来自 README 母题）

| 反模式 | 为什么错 | 正确做法 |
|--------|----------|----------|
| **为 3 个 skill 设计统一 schema** | 过早抽象 | v0 自由，重复 3+ 次再抽象 |
| **SKILL.md 没跑过就 commit** | 违反「跑一次才算数」 | Stage 4 必跑 |
| **省略「v0 已知不足」段** | 违反 v0 显式姿态 | 跑一次后必须补这一段 |
| **skill 替用户做判断** | 违反「工具替代判断处停下」 | Stage 2 问题 3 必须分流 |
| **写完美 frontmatter** | 违反 v0 心态 | 留下"已知不足"清单即可 |
| **混同"打扫卫生"和"规范化"** | 违反 README 二、第三节 | 规范化是显式阶段，独立计时 |

## §7. 何时升级到方案 B（6 阶段）

**触发条件（满足任一）：**
- `.claude/skills/` 下的 skill 数量 ≥ 5
- 出现 SKILL.md 之间结构漂移（同一个信息字段命名不一致）
- 「v0 已知不足」段出现重复模式（说明规范化时机到了）
- 出现「让我做 X skill」被同义反复提了 3+ 次

**升级动作：**
- 加 Stage 5：规范化扫（周期性对所有 .claude/skills/ 做结构漂移扫描）
- 加 Stage 6：v0 → v1 升级路径
- 仍不引入状态机（除非 skill 数量 ≥ 20）

## §8. 与本项目其他规范的关系

- **CLAUDE.md §0 决策原则：** Stage 2 的 3 个问题正是这条原则的实例化
- **CLAUDE.md §3 plans 工作流：** 复杂 skill 沉淀需要 plan（跨多文件 / 涉及现有 skills 互引时）
- **CONTRIBUTING.md git 节奏：** SKILL.md 沉淀按"一次一个意图"提交

## §9. 示范用法

用户：「我每次写一篇长笔记都要手动补 callout、mermaid、aliases、Dataview 查询，这个能不能做成 skill？」

按本方法论：

1. **Stage 1:** 接收——一句话 seed「给长笔记补 callout、mermaid、aliases、Dataview 查询」
2. **Stage 2:** 3 个问题
   - 痛点：长笔记的元数据补充是重复动作
   - 重复次数：「这篇是第 14 次了」→ 通过 3 次信号
   - 边界：callout/mermaid/aliases/Dataview 都是模板化的（资料收集）→ A
3. **Stage 3:** 命名候选 `vault-enhance`，写 SKILL.md
4. **Stage 4:** 在一篇真实长笔记上跑一次，记下「已知不足」

## §10. v0 已知不足（方法论自身的不足）

诚实记录方法论 v0 的不足：

- 3 个问题不覆盖所有形态（极复杂 skill 可能漏）
- 「跑一次」没有自动化，靠整理者（AI 协作者）自己保证
- 没有"skill 互引"机制
- 没有"skill 弃用"流程（只有 `status: deprecated` 字段）
- 命名约定是自由发挥的（升级到方案 B 时再规范）
- 还没在实际 skill 上完整跑过一遍——本方法论自身没经过 Stage 4 验证
````

（用 Write 工具创建。文件内容已在上方。）

- [ ] **Step 2: 验证文件存在且包含 6 个 § 节**

```bash
grep -E "^## §" /Users/charliepan/Downloads/grown-workflow/docs/methodology.md
```

Expected: 输出 11 行 `## §0.` 到 `## §10.`（§0 对应 README 母题映射，§1-§4 是 4 阶段，§5 是模板，§6 是反模式，§7 是升级触发，§8 是与其他规范关系，§9 是示范用法，§10 是 v0 已知不足）。

- [ ] **Step 3: 验证 6 个反模式行存在**

```bash
grep -c "^| \*\*" /Users/charliepan/Downloads/grown-workflow/docs/methodology.md
```

Expected: 输出 ≥ 6（每个反模式 1 个 `**` 粗体行）。也包含 README 母题对应表（5 行）和其他表项。

- [ ] **Step 4: 验证末尾含「v0 已知不足」段**

```bash
tail -10 /Users/charliepan/Downloads/grown-workflow/docs/methodology.md
```

Expected: 末 10 行包含「§10. v0 已知不足」段和至少 6 条 bullet points。

- [ ] **Step 5: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add docs/methodology.md
git commit -m "docs: add Skill curation methodology v0 (docs/methodology.md)

4-stage flow: receive → pain trace → crystallize SKILL.md → run-once.
Aligned with README motifs: 3-repetition signal, judgment-not-replaced,
v0 explicit known-gaps. Independent of CLAUDE.md, designed to evolve
into 6-stage variant when skill count >= 5 or structure drift emerges.

Methodology itself is v0 — it has not been run end-to-end on a real
skill yet (no Stage 4 verification on itself). v0 known-gaps section
documents this honestly."
```

---

## 验收标准（整体）

执行 Task 1 后验证：

- [ ] `docs/methodology.md` 存在
- [ ] 文件含 §0 到 §10 共 11 个节
- [ ] 4 阶段流程（§1-§4）齐全
- [ ] SKILL.md 模板（§5）有 frontmatter + 5 段骨架
- [ ] 6 个反模式表（§6）
- [ ] 4 个升级触发条件（§7）
- [ ] 末尾「v0 已知不足」段（§10）含 ≥ 6 条 bullet
- [ ] 1 个本地 commit 已完成（不 push）

```bash
# 最终验证
cd /Users/charliepan/Downloads/grown-workflow
git log --oneline -1
ls docs/methodology.md
grep -c "^## §" docs/methodology.md  # 应为 11
```

预期：1 个新 commit 的 subject 为：
`docs: add Skill curation methodology v0 (docs/methodology.md)`

**不要 push。** push 时机由用户决定。
