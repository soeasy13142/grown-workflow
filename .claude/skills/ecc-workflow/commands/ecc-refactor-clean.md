# 命令：`/ecc:refactor-clean` — 死代码清理

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:refactor-clean`。详见 [CREDITS.md](../../../CREDITS.md)。

## 何时用

- 发现未使用的变量、函数、导入
- 代码中有注释掉的死代码块
- 需要清理 `console.log` 等调试痕迹
- 代码异味积累到需要统一清理

## 本仓库约定

1. **清理前确认** — 自动清理可能删掉看似死代码但实际需要的逻辑，改动后人工确认
2. **清理后走 review** — 清理完成后走 `/ecc:code-review`
3. **一次一个意图** — 清理 commit 和功能 commit 分开，不混合

## 用法

```
在对话中直接输入：
/ecc:refactor-clean
```

ECC 会扫描当前代码范围，标记可清理的死代码。

## 参考

CLAUDE.md §5 DON'T 清单：
- 不写长函数（>50 行）→ 拆
- 不深度嵌套（>4 层）→ early return
- 不用 mutation → 改数据返回新对象
- 不留 console.log / debug 痕迹

---

*v0 — 适配 grown-workflow 的代码清理约定。*
