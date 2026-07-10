# 命令：`/ecc:build-fix` — 修复构建错误

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:build-fix`。详见 [CREDITS.md](../../../CREDITS.md)。

## 何时用

- 构建/编译报错
- 类型错误
- lint 错误
- 依赖冲突

## 本仓库约定

1. **先看错误信息** — 命令触发前，确保错误信息已在上下文中
2. **修复后走 review** — 修复完成后走 `/ecc:code-review` 确认改动正确
3. **不重复 fix** — 如果同一个问题被 `/ecc:code-review` 标记过，直接引用 review 结果

## 用法

```
在对话中直接输入：
/ecc:build-fix

然后粘贴或描述构建错误。
```

ECC 会分析错误根因并建议修复方案。

## 注意

- `/ecc:build-fix` 定位的是构建时错误，不是运行时 bug
- 运行时 bug 请描述上下文，不要用此命令

---

*v0 — 适配 grown-workflow 的构建修复约定。*
