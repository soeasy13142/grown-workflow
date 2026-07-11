### Task 6: 在 CONTRIBUTING.md 末尾补充 push 规范化细则

**Files:**
- Modify: `CONTRIBUTING.md`（末尾追加，不修改既有内容）

**Interfaces:**
- Consumes: Task 1-4 已就位的脚手架
- Produces: CONTRIBUTING.md 含 git push 前 squash / rebase 流程

- [ ] **Step 1: 在 `CONTRIBUTING.md` 末尾追加以下内容**

在文件 `/Users/charliepan/Downloads/grown-workflow/CONTRIBUTING.md` 的**末尾**追加：

````markdown


## Git Push 规范化

本地提交按 `一次一个意图` 的节奏进行（高频、小颗粒）。push 到远端前必须整理 commit 历史：

### 推荐流程

```bash
# 1. 确认 main 是最新的
git fetch origin
git checkout main
git pull --rebase

# 2. 切到你的功能分支，整理 commit
git checkout feature/your-branch
git rebase -i main
# 把除第一个外的 commit 标记为 squash / fixup

# 3. 推送（首次推送加 -u）
git push -u origin feature/your-branch

# 或合并到 main（merge 模式任选，建议 fast-forward 或 squash merge）
```

### 原则

- push 出去的 commit 列表应是一个连贯的「意图批次」，不是本地细粒度 commit 流
- push 前自查：`git log origin/main..HEAD` 应是可独立检视的几个 commit
- 如果一个功能分支上本地有 10+ 个 commit，先 rebase 整理，再 push
````

追加后，最后几行应为：

```
... (原有内容) ...

## Git Push 规范化

本地提交按 `一次一个意图` 的节奏进行（高频、小颗粒）...
```

- [ ] **Step 2: 验证追加成功**

```bash
tail -5 /Users/charliepan/Downloads/grown-workflow/CONTRIBUTING.md
```

Expected: 末 5 行包含 `## Git Push 规范化`。

- [ ] **Step 3: 验证 CONTRIBUTING 主体内容未被改动**

```bash
wc -l /Users/charliepan/Downloads/grown-workflow/CONTRIBUTING.md
```

Expected: 比修改前略增（约 +30 行）。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add CONTRIBUTING.md
git commit -m "docs: detail git push normalization in CONTRIBUTING.md"
```

---

## 验收标准（整体）

执行全部 6 个任务后，验证：

- [ ] 仓库根存在 `CLAUDE.md`，含 `§0` 到 `§7` 共 8 节
- [ ] `docs/plans/README.md` 存在且含「何时写 plan」「命名」「模板」「不要做」四节
- [ ] `.claude/skills/.gitkeep` 与 `.claude/scripts/.gitkeep` 存在
- [ ] 仓库根 `skills/`、`scripts/` 已不存在
- [ ] `README.md` 末尾包含「附：给 AI 协作者的契约」段
- [ ] `CONTRIBUTING.md` 末尾包含「Git Push 规范化」段
- [ ] git log 显示 6 个新 commit（commit 1-6）

```bash
# 最终验证
cd /Users/charliepan/Downloads/grown-workflow
git log --oneline -10
ls CLAUDE.md docs/plans/README.md .claude/skills/.gitkeep .claude/scripts/.gitkeep
ls skills/ scripts/ 2>&1 | grep -E "No such"  # 应有 No such file or directory
```

预期：6 个新 commit 的 subject 分别为：
- `chore: add .claude/skills/ and .claude/scripts/ scaffolds`
- `chore: remove root skills/ and scripts/ (consolidated into .claude/)`
- `docs: add docs/plans/ with README template`
- `docs: add CLAUDE.md (AI collaboration contract)`
- `docs: link README.md to CLAUDE.md`
- `docs: detail git push normalization in CONTRIBUTING.md`

**不要 push。** push 时机由用户决定。
