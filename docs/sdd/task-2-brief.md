### Task 2: 删除仓库根 `skills/` 和 `scripts/`（已统一到 `.claude/` 下）

**Files:**
- Delete: `skills/` (含 `.gitkeep`)
- Delete: `scripts/` (含 `.gitkeep`)

**Interfaces:**
- Consumes: Task 1 已建 `.claude/skills/`、`.claude/scripts/`
- Produces: 仓库根不再有 `skills/`、`scripts/`；语义统一到 `.claude/` 下

- [ ] **Step 1: 用 git rm 删除仓库根 `skills/`**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git rm -r skills/
```

Expected: 输出 `rm 'skills/.gitkeep'`。

- [ ] **Step 2: 用 git rm 删除仓库根 `scripts/`**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git rm -r scripts/
```

Expected: 输出 `rm 'scripts/.gitkeep'`。

- [ ] **Step 3: 验证删除**

```bash
ls /Users/charliepan/Downloads/grown-workflow/ | grep -E "^(skills|scripts)$"
```

Expected: 无输出（仓库根不再有 skills/、scripts/）。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git commit -m "chore: remove root skills/ and scripts/ (consolidated into .claude/)"
```

---

