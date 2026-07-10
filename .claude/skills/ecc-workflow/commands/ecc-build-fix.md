# 命令：`/ecc:build-fix` — 修复构建错误

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/ecc:build-fix`。
> 详见 [CREDITS.md](../../../CREDITS.md)。  ✅ v0 · 2026-07-10

## 何时用

- 构建/编译报错
- 类型错误
- lint 错误
- 依赖冲突或缺失

## 真实示例

**场景：** 运行测试时发现依赖缺失。

```
你： /ecc:build-fix
    运行 npm test 报错：
    Error: Cannot find module 'jest'
    Require stack:
    - C:\Users\...\grown-workflow\package.json

ECC： 分析...
      检测到缺少 jest 依赖。
      建议：npm install --save-dev jest
      检查 package.json 中 scripts.test 配置...
```

**产出物：** 构建错误被修复，`npm test` 可正常运行。

## 本仓库约定

1. **先看错误信息** — 触发前确保完整错误信息已在上下文中
2. **修复后走 review** — 修复完走 `/ecc:code-review` 确认改动正确
3. **不重复 fix** — 如果同一个问题被 `/ecc:code-review` 标记过，直接引用 review 结果

## 边界与陷阱

| 情况 | 处理 |
|------|------|
| 错误是环境问题（PATH、权限） | ECC 可能无法直接修复，需人工介入 |
| 修复引入了新问题 | 回退修复，重新分析根因 |
| 多个错误互相依赖 | 按依赖顺序逐个修复 |
| 运行时 bug（非构建时） | `/ecc:build-fix` 不适用，描述上下文手工排查 |

## 验证

修复后检查：

- ✅ 构建命令可正常运行（`npm run build` / `make` / 等）
- ✅ 无新增 lint 警告
- ✅ 原有功能不受影响（跑一遍测试）

## 交叉引用

| 相关命令 | 关系 |
|---------|------|
| `/ecc:code-review` | 修复后 review 确认改动 |
| `/ecc:refactor-clean` | 如果修复中引入了冗余代码 |
| `/ecc:test-coverage` | 修复后确认测试仍通过 |

## 已知不足（v0）

- 依赖 ECC 对项目构建工具链的识别能力，非标准构建工具可能无法自动修复
- 本仓库当前无实际构建流程，此命令首次调用时需验证兼容性
- Windows 环境差异可能导致修复方案需微调

## 历史

- 2026-07-10: v0 从 ECC 精选纳入，首次提交（commit `d12eef9`）
- 2026-07-10: v0 深度升级——加真实示例、边界与陷阱表、验证检查清单、交叉引用
