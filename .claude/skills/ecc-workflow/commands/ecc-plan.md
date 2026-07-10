# 命令：`/ecc:plan` — 功能规划与任务拆解

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:plan`。
> 详见 [CREDITS.md](../../../CREDITS.md)。  ✅ v0 · 2026-07-10

## 何时用

- 跨多文件 / 多阶段 / 含架构决策 / 涉及不熟悉库的任务
- 你感觉"这个有点复杂，不知道从哪下手"
- 接到一个模糊的需求，需要拆解成可执行的步骤

## 真实示例

**场景：** 想为本仓库新增一个 `terraform-skill`，需要确定结构、内容、文件位置。

```
你： /ecc:plan
    我想给 grown-workflow 新增一个 terraform skill，
    参考 obsidian-vault-enhance 的结构，放在 .claude/skills/terraform-skill/ 下。

ECC： 开始拆解...
      Phase 1: 确定 skill 类型
      Phase 2: 参考 obsidian-vault-enhance 的文件结构
      Phase 3: 写 SKILL.md 骨架
      Phase 4: 写命令文档（如有需要）
      ...
```

**产出物：** `docs/plans/2026-07-10-terraform-skill.md`

## 本仓库约定

1. **plan 位置** — `docs/plans/YYYY-MM-DD-<topic>.md`
2. **触发条件** — 满足 CLAUDE.md §3 任何一条即走 plan 流程
3. **plan 是活文档** — 实施中持续更新，完成时附回顾
4. **简单任务可跳过** — 单文件 / 纯文档小改不需要 plan

## 边界与陷阱

| 情况 | 处理 |
|------|------|
| 任务极其简单（改一行 README） | 跳过 `/ecc:plan`，直接做 |
| ECC 拆出的 plan 和你的理解有偏差 | 在对话中纠正，ECC 会调整 |
| plan 写到一半发现需求不明确 | 停下来，用 AskUserQuestion 问用户 |
| 多个 plan 交叉依赖 | 先拆解子任务，各自 plan，标注依赖关系 |

## 验证

跑完 `/ecc:plan` 后检查：

- ✅ `docs/plans/` 下生成了 plan 文件
- ✅ plan 文件包含：背景、拆解步骤、产出物清单
- ✅ 你理解了每一步要做什么

## 交叉引用

| 相关命令/文档 | 关系 |
|-------------|------|
| `/tdd` | plan 写完后的下一步（如果需要新功能） |
| `/ecc:code-review` | plan 涉及到的代码变更最终需要 review |
| CLAUDE.md §3 | Plans 工作流的补充规则 |
| `docs/principles.md` | 计划本质的原则讨论 |

## 已知不足（v0）

- plan 文件名中的 `YYYY-MM-DD` 硬编码日期，跨多日 plan 需手动调整
- 依赖 ECC 的拆解能力，复杂架构决策仍需人工判断
- 本仓库 `docs/plans/` 目前为空（尚未有 plan 落地），第一个 plan 将验证这个路径

## 历史

- 2026-07-10: v0 从 ECC 精选纳入，首次提交（commit `d12eef9`）
- 2026-07-10: v0 深度升级——加真实示例、边界与陷阱表、验证检查清单、交叉引用
