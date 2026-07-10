# 命令：`/tdd` — TDD 工作流

> 本命令基于 ECC（affaan-m/ECC, MIT）的 `/tdd`。
> 详见 [CREDITS.md](../../../CREDITS.md)。  ✅ v0 · 2026-07-10

## 何时用

- 新功能开发，有明确输入/输出边界的模块
- 已有功能需要增加测试覆盖
- bug 修复：先写一个暴露 bug 的测试，再修

## 真实示例

**场景：** 为本仓库的工具函数写一个 `slugify` 函数，走 TDD。

```
你： /tdd
    我想在 .claude/scripts/utils.sh 里加一个 slugify 函数，
    把中文字符串转成 kebab-case 的英文 slug。

ECC： 进入 TDD 循环...
       RED: 先写测试用例...
         test_slugify_basic: "Hello World" → "hello-world"
         test_slugify_chinese: "功能规划" → "gong-neng-gui-hua"
       GREEN: 实现 slugify 让测试通过...
       IMPROVE: 重构...
```

**产出物：**
- 测试文件：`.claude/scripts/tests/test_utils.sh`
- 实现文件：`.claude/scripts/utils.sh`

## 本仓库约定

1. **先写测试** — 新功能必须先从测试用例开始
2. **目标覆盖率 ≥ 80%** — 见 `.claude/rules/common/testing.md`
3. **测试不是凑数** — 不要仅为通过覆盖率而写无效断言
4. **ECC 的 /tdd 流程** — 自动引导：写测试 → 跑 → 红 → 写实现 → 绿 → 重构

## 边界与陷阱

| 情况 | 处理 |
|------|------|
| 功能不需要测试（纯配置改动） | 跳过 `/tdd`，走 `/ecc:code-review` 即可 |
| 测试写完后发现设计有问题 | 回退到 `/ecc:plan` 重新规划 |
| /tdd 生成的测试不够全面 | 手动补充边界用例，再跑 `/ecc:test-coverage` |
| 纯探索性任务、架构设计 | `/tdd` 不适用，走 `/ecc:plan` |

## 验证

跑完 `/tdd` 后检查：

- ✅ 测试通过（RED → GREEN 循环完成）
- ✅ 测试覆盖了正常路径 + 至少一个边界路径
- ✅ 实现代码经过了重构（IMPROVE 阶段）

## 交叉引用

| 相关命令 | 关系 |
|---------|------|
| `/ecc:plan` | TDD 之前应先有 plan（除非任务极其简单） |
| `/ecc:test-coverage` | 完成后检查覆盖率是否 ≥ 80% |
| `/ecc:code-review` | TDD 实现完成后走 review |

## 已知不足（v0）

- 本仓库尚无实际运行的测试框架，/tdd 首次调用需要先搭建测试基础设施
- ECC 的 /tdd 对非 JavaScript/Python 项目的支持取决于 ECC 版本

## 历史

- 2026-07-10: v0 从 ECC 精选纳入，首次提交（commit `d12eef9`）
- 2026-07-10: v0 深度升级——加真实示例、边界与陷阱表、验证检查清单、交叉引用
