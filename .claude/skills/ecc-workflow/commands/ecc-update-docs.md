# 命令：`/ecc:update-docs` — 文档更新

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:update-docs`。
> 详见 [CREDITS.md](../../../CREDITS.md)。  ✅ v0 · 2026-07-10

## 何时用

- 代码变更后文档不同步
- 新增功能需要补充文档
- API / 接口签名变更
- README 或 CLAUDE.md 需要同步更新
- 计划或设计文档需要跟进实施状态

## 真实示例

**场景：** 新增了一个 skill 后需要更新文档索引。

```
你： /ecc:update-docs
    我新加了 .claude/skills/terraform-skill/，需要更新文档。

ECC： 扫描变更...
      检测到新增:
      - .claude/skills/terraform-skill/SKILL.md
      - .claude/skills/terraform-skill/commands/plan.md
      建议更新:
      1. CLAUDE.md §2 ECC 命令速查表——不适用（非 ECC 命令）
      2. .claude/skills/README.md ——需添加 terraform-skill 条目
      3. CREDITS.md ——无需改动
```

**产出物：** `.claude/skills/README.md` 更新，新增 terraform-skill 条目。

## 本仓库约定

1. **文档即代码** — 文档变更和代码变更在同一个 commit 中
2. **目录约定** — 外部文档走 `docs/`，AI 协作产物走 `.claude/`
3. **归属声明不可省略** — 引用外部项目时，在 `CREDITS.md` 中记录

## 边界与陷阱

| 情况 | 处理 |
|------|------|
| 文档变更范围很大 | 分批更新，每批独立 commit |
| 文档与代码存在深度绑定 | 同时更新，确保原子性 |
| 若干文档互相引用 | 更新时要保持交叉引用的一致性 |
| 纯文档仓库（如本仓库） | `/ecc:update-docs` 是高频命令 |

## 验证

更新后检查：

- ✅ 新增/修改的文档内容准确
- ✅ 交叉引用链接有效
- ✅ CREDITS.md 中的归属声明完整（如有外部引用）

## 交叉引用

| 相关命令/文档 | 关系 |
|-------------|------|
| `/ecc:code-review` | 文档更新后走 review |
| CLAUDE.md §6 | 目录约定（文档走 `docs/`，skill 走 `.claude/`） |
| `docs/methodology.md` | Skill 整理方法论（新增 skill 时参考） |

## 已知不足（v0）

- 本仓库是文档项目，此命令的使用频率可能高于其他命令
- ECC 可能无法检测到所有需要更新的文档链接
- 中文文档的中英文版本同步依赖人工判断

## 历史

- 2026-07-10: v0 从 ECC 精选纳入，首次提交（commit `d12eef9`）
- 2026-07-10: v0 深度升级——加真实示例、边界与陷阱表、验证检查清单、交叉引用
