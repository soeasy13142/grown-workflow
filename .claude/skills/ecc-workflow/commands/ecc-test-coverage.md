# 命令：`/ecc:test-coverage` — 覆盖率分析

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:test-coverage`。详见 [CREDITS.md](../../../CREDITS.md)。

## 何时用

- 功能开发完成后检查覆盖率
- 发现某模块测试不足时
- CI 流水线中覆盖率门禁失败时

## 本仓库约定

1. **目标覆盖率 ≥ 80%** — 见 `.claude/rules/common/testing.md`
2. **不是数字游戏** — 不要仅为通过覆盖率而写无效断言。真实覆盖行为比数字重要
3. **核心模块优先** — 工具函数、数据层、API 路由覆盖优先级最高；UI 组件次之

## 用法

```
在对话中直接输入：
/ecc:test-coverage
```

ECC 会分析当前测试覆盖率，标记未覆盖的分支和边界。

## 配合使用

| 发现 | 处理 |
|------|------|
| 覆盖率不足 | `/tdd` 补测试 |
| 死代码/不可测代码 | `/ecc:refactor-clean` |
| 修复后再次检查 | `/ecc:test-coverage` |

---

*v0 — 适配 grown-workflow 的覆盖率和约定。*
