# 命令：`/ecc:plan` — 功能规划与任务拆解

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:plan`。详见 [CREDITS.md](../../../CREDITS.md)。

## 何时用

跨多文件 / 多阶段 / 含架构决策 / 涉及不熟悉库的任务。

## 本仓库约定

1. **plan 位置** — plan 文件统一写到 `docs/plans/YYYY-MM-DD-<topic>.md`
2. **触发条件** — 满足 CLAUDE.md §3 的任何一条即走 plan 流程
3. **plan 是活文档** — 实施中持续更新，完成时附回顾（见 `docs/principles.md`）
4. **简单任务不需要 plan** — 单文件、纯文档小改可以跳过

## 用法

```
在对话中直接输入：
/ecc:plan

然后描述任务背景。
```

ECC 会引导你完成功能拆解和计划编写。

## 输出产物

- `docs/plans/<date>-<topic>.md` — plan 文档
- 实施完成后更新 plan 文件，添加回顾总结

---

*v0 — 适配 grown-workflow 的 plan 工作流约定。*
