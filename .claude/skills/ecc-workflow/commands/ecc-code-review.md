# 命令：`/ecc:code-review` — 代码质量审查

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:code-review`。
> 详见 [CREDITS.md](../../../CREDITS.md)。  ✅ v0 · 2026-07-10

## 何时用

- 合并到主分支 / 共享分支前
- 复杂功能实现后
- 收到外部 PR 时
- 定期代码健康检查

## 真实示例

**场景：** 提交 ECC 工作流文档后，合并到 main 前做 review。

```
你： /ecc:code-review
    我刚刚改了 .claude/skills/ecc-workflow/ 下的文档，
    准备合并到 main，先 review 一下。

ECC： 分析 diff...
      ✅ 文档结构清晰
      ✅ 归属声明完整
      ⚠️ CLAUDE.md §2 的表格第三列是相对路径，
         建议确认渲染后链接可点击
      ℹ️ CREDITS.md 与 SKILL.md 的引用一致
```

## 本仓库约定

1. **合并前必须有 review** — CLAUDE.md §5 强制要求
2. **review 走 ECC 优先** — 备选方案是用 `code-reviewer` Agent
3. **review 维度** — 正确性、可维护性、性能、安全
4. **review 出的问题必须解决或回复** — 不能不处理就合并

## 边界与陷阱

| 情况 | 处理 |
|------|------|
| review 指出大量问题 | 分批修复，每批修复后重新 review |
| review 误报 | 确认误报后回复解释，标记为已解决 |
| 紧急修复需要跳过 review | 例外情况，合并后补 review |
| ECC review 深度不够 | 换用 `code-reviewer` Agent 做第二遍 |

## 验证

跑完 `/ecc:code-review` 后检查：

- ✅ review 报告已阅读
- ✅ 所有标记的问题已被处理（修复 / 回复解释）
- ✅ 无 P0/P1 级别的未解决问题

## 交叉引用

| 相关命令 | 关系 |
|---------|------|
| `/tdd` | review 前建议已走 TDD |
| `/ecc:build-fix` | review 指出构建问题后修复 |
| `/ecc:refactor-clean` | review 指出代码异味后清理 |
| `/ecc:test-coverage` | review 指出测试不足后补充 |
| `code-reviewer Agent` | ECC review 的备选方案 |

## 已知不足（v0）

- ECC review 依赖当前 git diff，未提交的更改不会被 review
- review 质量受限于 ECC 版本对项目语言的支持程度
- 对于纯文档 PR，review 收益有限，可酌情跳过

## 历史

- 2026-07-10: v0 从 ECC 精选纳入，首次提交（commit `d12eef9`）
- 2026-07-10: v0 深度升级——加真实示例、边界与陷阱表、验证检查清单、交叉引用
