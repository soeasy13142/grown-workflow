---
name: consolidating-docs
description: Use when a project's CLAUDE.md is too verbose (>200 lines), when doc files duplicate each other's content, when CONTRIBUTING.md is not at project root, when doc file names don't follow consistent conventions, or when .superpowers/ or other agent working files are tracked in git.
---

# Consolidating Docs

## Overview

Each doc file serves one purpose and cross-references others. CLAUDE.md is agent onboarding (~150 lines), not a full manual.

## When to Use

- CLAUDE.md >200 lines or duplicates README content
- CONTRIBUTING.md under `dev/` or `docs/` instead of root
- Agent artifacts (`.superpowers/`, `.claude/worktrees/`) tracked in git
- Cross-references between doc files are stale

## When NOT to Use

- No docs exist yet
- One file needs a trivial edit
- Docs are already clean

## CLAUDE.md — Write This Structure Exactly

Do NOT edit the existing file section by section. **Write a new file** with exactly these 7 sections in this order. Each section header must match one of the 7 below.

### 1. Identity (2-4 lines)

```markdown
# <Project>

<one-line description>. See [README.md](README.md) for full intro.

- **Tech**: <language> <version>, <framework>
- **Tests**: <framework>, <count> tests, <coverage>% coverage
```

### 2. Quick Start (2-5 commands)

```markdown
## Quick Start

\`\`\`bash
<clone>
<install>
<configure>
<run tests>
\`\`\`
```

Keep this even if it partly overlaps README. It exists for agent convenience.

### 3. Key Conventions (5-10 bullets)

```markdown
## Key Conventions

- **TDD required**: RED → GREEN → IMPROVE
- **Type hints**: required on all public functions
- **Immutability**: prefer new objects over mutation
- **Coverage ≥ <N>%**: verify with `pytest --cov`
- **No silent failures**: handle errors explicitly
- **Config via env**: never hardcode secrets
```

### 4. Module Boundaries (table, or skip if 1 file)

```markdown
## Module Boundaries

| Module | Responsibility | Must NOT import |
|--------|---------------|-----------------|
| `a.py` | <role> | <avoid> |
| `b.py` | <role> | <avoid> |
```

### 5. DO / DON'T (~6 each)

```markdown
## DO / DON'T

### ✅ DO
- DO <rule>

### ❌ DON'T
- DON'T <rule>
```

### 6. Architecture (compact, or skip if trivial)

```markdown
## Architecture

\`\`\`
<≤10 line ASCII diagram>
\`\`\`

- <invariant 1>
```

### 7. Reference (table)

```markdown
## Reference

| Doc | For |
|-----|-----|
| `README.md` | Project overview |
| `CONTRIBUTING.md` | Developer guide |
| `docs/deployment.md` | Deployment |
```

**Content to omit** (belongs in other files, not CLAUDE.md): project layout tree, "how it works" narrative, features list, deployment commands, security specs list, ECC/plugin tables, `.claude/` directory tree.

## File Cleanup

| Situation | Action |
|-----------|--------|
| CONTRIBUTING.md in `dev/`/`docs/` | `git mv` to root; `rmdir dev/` if empty |
| `.superpowers/`, `.claude/worktrees/` tracked | Add to `.gitignore`; `git rm --cached`; leave files on disk |
| `docs/README.md` is narrative | Rewrite as short index table only |
| `plans/` historical files | Never touch |
| Stale cross-references | `grep -rn "old-path" --include="*.md" .` → update |

## Checklist

- [ ] CLAUDE.md has all 7 sections (1 Identity, 2 Quick Start, 3 Conventions, 4 Boundaries, 5 DO/DON'T, 6 Architecture, 7 Reference) — in that order
- [ ] CONTRIBUTING.md at root, empty dev/ removed
- [ ] `.superpowers/` in .gitignore (not deleted)
- [ ] `plans/` untouched
- [ ] Tests pass, `git status` clean
