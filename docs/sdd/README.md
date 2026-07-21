# `docs/sdd/` 目录说明

> SDD（spec-driven development）过程产物。原位于 `.superpowers/sdd/`，2026-07-11 迁入本目录。
> **commit 入仓**。

> **定位：本仓库**自身建设**的过程记录，不是要分享的核心内容。**
>
> SDD 任务记录的是本仓库如何用 SDD 方法论建设自身——Task 1-6 全是在构建这个仓库本身（创建 CLAUDE.md、整理目录结构等）。这是方法论实跑的副产品，属于建设记录，不属于 skill/工作流成果。

## 文件类型

| 类型 | 命名 | 说明 |
|------|------|------|
| 任务简报 | `task-<n>-brief.md` | 每个 SDD 任务的输入 |
| 任务报告 | `task-<n>-report.md` | 每个 SDD 任务的产出 |
| 评审 diff | `review-<from>..<to>.diff` | 两次 commit 之间的代码评审记录 |
| 进度 | `progress.md` | 当前 SDD 流程的进度 |

## 维护要点

- 数字编号按 SDD 流程顺序递增
- 此前目录内的 `.gitignore`（内容 `*`）已在迁移时删除，文件现正常入仓