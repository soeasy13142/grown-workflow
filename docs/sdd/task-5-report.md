# Task 5 Report: 在 README.md 末尾增加指向 CLAUDE.md 的引用段

## What was implemented

Appended a new section `## 附：给 AI 协作者的契约` to the end of `/Users/charliepan/Downloads/grown-workflow/README.md`. The new section informs readers that the AI collaboration contract lives in `CLAUDE.md` (auto-loaded by Claude Code), and points to that file for decision/git/ECC/DO/DON'T conventions.

The append used the Edit tool with `old_string` = the file's last existing line ("让方法长出来。能被重写的方法，比不会过期的方法，更适合陪伴一段长跑。") and `new_string` = that same line + one blank separator + the new section content. No existing content was modified.

## Files changed

- `README.md` — appended 4 lines (1 blank + 1 header + 1 blank + 1 content). No deletions, no modifications to existing lines.

## Verification commands and outputs

### 1. `tail -5 README.md`
```
让方法长出来。能被重写的方法，比不会过期的方法，更适合陪伴一段长跑。

## 附：给 AI 协作者的契约

本仓库的 AI 协作主契约在 [`CLAUDE.md`](./CLAUDE.md)。Claude Code 在本仓库内工作时自动加载该文件。涉及决策、git 流程、ECC 命令、DO/DON'T 等协作约定，以 `CLAUDE.md` 为准。
```
Confirmed: the new section header is present at the end of the file.

### 2. `wc -l README.md`
- Before: 57 lines
- After: 61 lines
- Delta: +4 lines (brief expected "约 +5 行"; +4 is the actual section content — 1 blank + header + 1 blank + paragraph — and is within tolerance of "约")

### 3. `git diff HEAD~1 -- README.md`
```
diff --git a/README.md b/README.md
index 9719961..839b4e9 100644
--- a/README.md
+++ b/README.md
@@ -55,3 +55,7 @@ v0 的正确姿态：先写一份能用的版本，把已知的不足有意地
 反过来读一遍：不要试图站在原地规划一条完美的协作路径。先把 v0 写出来，让规范化在长跑中自然出现的位置显形，让工具在痛点真的冒头时再沉下去。
 
 让方法长出来。能被重写的方法，比不会过期的方法，更适合陪伴一段长跑。
+
+## 附：给 AI 协作者的契约
+
+本仓库的 AI 协作主契约在 [`CLAUDE.md`](./CLAUDE.md)。Claude Code 在本仓库内工作时自动加载该文件。涉及决策、git 流程、ECC 命令、DO/DON'T 等协作约定，以 `CLAUDE.md` 为准。
```
Confirmed: ONLY additions, no edits to existing content. The `@@ -55,3 +55,7 @@` hunk header shows 3 unchanged context lines on the left and 7 lines on the right (3 unchanged + 4 added).

### 4. `git log --oneline -3`
```
4218f81 docs: link README.md to CLAUDE.md
aab7e3e docs: add CLAUDE.md (AI collaboration contract)
3002923 docs: add docs/plans/ with README template
```
- New commit `4218f81` is on top of Task 4's `aab7e3e`.
- Subject matches brief exactly: `docs: link README.md to CLAUDE.md`.
- No push performed (local only, per global constraint).

## Self-review findings

- [x] README.md existing content is byte-identical to before — diff confirms only `+` lines, no `-` lines.
- [x] New section `## 附：给 AI 协作者的契约` appears at end of file.
- [x] Line count increased by 4 lines (brief said "约 +5 行" — within tolerance).
- [x] Single commit with exact subject from brief: `docs: link README.md to CLAUDE.md`.
- [x] CLAUDE.md NOT touched — only `README.md` in the changeset.
- [x] No push to remote (local commit only).

## Concerns

None. The line count delta is +4 rather than the brief's "约 +5", but this is the natural size of the appended section (1 blank separator + 1 H2 header + 1 blank line + 1 paragraph = 4 lines). The brief's "约 +5" appears to be a rough estimate; +4 is the actual content as specified.

If a reviewer wants exactly +5, an extra trailing blank line could be added, but that would create a trailing-blank-line at end of file and was not specified in the brief's expected output.
