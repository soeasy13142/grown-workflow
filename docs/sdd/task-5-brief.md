### Task 5: 在 README.md 末尾增加指向 CLAUDE.md 的引用段

**Files:**
- Modify: `README.md`（末尾追加，不修改既有内容）

**Interfaces:**
- Consumes: Task 4 产出的 CLAUDE.md
- Produces: README.md 末尾新增一节，链接到 CLAUDE.md

- [ ] **Step 1: 在 `README.md` 末尾追加以下内容**

在文件 `/Users/charliepan/Downloads/grown-workflow/README.md` 的**末尾**追加（用 Edit 工具，old_string 为文件现有最后一段，new_string 为「现有末尾 + 新增内容」）：

````markdown


## 附：给 AI 协作者的契约

本仓库的 AI 协作主契约在 [`CLAUDE.md`](./CLAUDE.md)。Claude Code 在本仓库内工作时自动加载该文件。涉及决策、git 流程、ECC 命令、DO/DON'T 等协作约定，以 `CLAUDE.md` 为准。
````

追加后，最后几行应为：

```
... (原有内容) ...

## 附：给 AI 协作者的契约

本仓库的 AI 协作主契约在 [`CLAUDE.md`](./CLAUDE.md)。Claude Code 在本仓库内工作时自动加载该文件。涉及决策、git 流程、ECC 命令、DO/DON'T 等协作约定，以 `CLAUDE.md` 为准。
```

- [ ] **Step 2: 验证追加成功**

```bash
tail -5 /Users/charliepan/Downloads/grown-workflow/README.md
```

Expected: 末 5 行包含 `## 附：给 AI 协作者的契约`。

- [ ] **Step 3: 验证 README 主体内容未被改动（行数应略增）**

```bash
wc -l /Users/charliepan/Downloads/grown-workflow/README.md
```

Expected: 比修改前略增（约 +5 行）。

- [ ] **Step 4: 提交**

```bash
cd /Users/charliepan/Downloads/grown-workflow
git add README.md
git commit -m "docs: link README.md to CLAUDE.md"
```

---

