# 命令：`/ecc:code-review` — 代码质量审查

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:code-review`。详见 [CREDITS.md](../../../CREDITS.md)。

## 何时用

- 合并到主分支 / 共享分支前
- 复杂功能实现后
- 收到 PR 时

## 本仓库约定

1. **合并前必须有 review** — CLAUDE.md §5 强制要求
2. **review 走 ECC** — 用手工 `code-reviewer` Agent 作为备选，优先用 `/ecc:code-review`
3. **review 维度** — 正确性、可维护性、性能、安全

## 用法

```
在对话中直接输入：
/ecc:code-review

ECC 会自动分析当前 diff 并输出审查结果。
```

## 配合使用

| 场景 | 命令 |
|------|------|
| 修复 review 指出的问题 | `/ecc:build-fix` 或 `/ecc:refactor-clean` |
| review 后补充测试 | `/tdd` |
| review 后检查覆盖率 | `/ecc:test-coverage` |

---

*v0 — 适配 grown-workflow 的 code-review 流程。*
