### Task 3: 新增 `docs/plans/` 文件夹及 README 模板

**Files:**
- Create: `docs/plans/.gitkeep`
- Create: `docs/plans/README.md`

**Interfaces:**
- Consumes: nothing
- Produces: plans 文件夹与说明文档；为后续实施性 plan 提供位置与模板

- [ ] **Step 1: 创建 `docs/plans/.gitkeep`**

```bash
mkdir -p /Users/charliepan/Downloads/grown-workflow/docs/plans
touch /Users/charliepan/Downloads/grown-workflow/docs/plans/.gitkeep
```

- [ ] **Step 2: 创建 `docs/plans/README.md`，内容如下**

写入文件 `/Users/charliepan/Downloads/grown-workflow/docs/plans/README.md`，内容为：

````markdown
# Plans

复杂任务的 plan 文档存放处。Plan 是活记录，不是出发前的门票。

## 何时写 plan

满足以下任一条件：

- 跨多文件
- 多阶段（分析 → 设计 → 实施 → 验证）
- 跨多日
- 含架构决策
- 涉及不熟悉的库 / 框架 / API

## 命名

`YYYY-MM-DD-<topic>.md`，例如 `2026-07-10-claude-md-init.md`。

## 模板

1. 目标（一句话）
2. 范围（做什么 / 不做什么）
3. 步骤
4. 决策记录（实施中改了什么、为什么）
5. 回顾（完成后）

## 不要做

- 不要把 plan 写进 CLAUDE.md 或其他文件
- 不要在 plan 之外的地方藏代码片段
- 不要 plan 与实施脱钩——plan 是活记录，改 plan 是正常的
````

（用 Write 工具创建。文件内容已在上方。）

- [ ] **Step 3: 验证文件内容**

```bash
head -5 /Users/charliepan/Downloads/grown-workflow/docs/plans/README.md
```

Expected: 首 5 行包含 `# Plans` 与 `## 何时写 plan`。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add docs/plans/
git commit -m "docs: add docs/plans/ with README template"
```

---

