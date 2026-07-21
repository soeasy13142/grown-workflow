# grown-workflow

[![GitHub](https://img.shields.io/badge/GitHub-soeasy13142/grown--workflow-181717?logo=github)](https://github.com/soeasy13142/grown-workflow)
[![License](https://img.shields.io/github/license/soeasy13142/grown-workflow?color=blue)](LICENSE)

[简体中文](.claude/README.md) | [**English**](.claude/README.en.md)

> **Let AI collaboration start with scaffolding, interleave normalization with progress, and grow tools from pain points.**

---

## About This Project

**grown-workflow** is not a project that produces software. It is a **meta-project** — a methodology and tooling kit for *how to structure AI-augmented collaboration* — and it is itself a living demonstration of its own principles.

The methodology was not designed upfront and then built. It *grew* from 100+ commits of real practice, and that journey was distilled into the essay in [`README.md`](../README.md). The repository's structure itself is proof of the method.

### Three Core Themes

| Theme | In a Nutshell |
|-------|---------------|
| **Scaffolding Before Project** | Write the AI collaboration contract (CLAUDE.md) as v0 from day one; accept that it will be rewritten |
| **Progress Alternates With Normalization** | Advance → pause to normalize → advance again; normalization is an explicit phase, not tidying up |
| **Tools Grow From Pain Points** | Only formalize a tool after the 3-repetition signal; tools chase pain, pain chases context |

See the full essay in [`README.md`](../README.md). Philosophical principles in [`docs/principles.md`](../docs/principles.md) (Chinese only).

---

## Skills

Project skills live under `.claude/skills/<name>/`. Each skill has a SKILL.md core document and supporting materials.

### ecc-workflow — Curated ECC Workflow

**Purpose** — A curated set of 8 commands from [ECC (Enhanced Claude Capabilities)](https://github.com/affaan-m/ECC), wrapped with project-local conventions and an orchestration guide.

**Usage** — Pick a starting command from the scenario table; commands can be chained into a complete workflow:

| Command | Purpose |
|---------|---------|
| `/ecc:plan` | Feature planning and task decomposition |
| `/tdd` | Test-driven development |
| `/ecc:code-review` | Code quality review |
| `/ecc:build-fix` | Fix build errors |
| `/ecc:refactor-clean` | Dead code cleanup |
| `/e2e` | End-to-end testing |
| `/ecc:test-coverage` | Coverage analysis |
| `/ecc:update-docs` | Documentation updates |

**Links** — [ECC Official Repository](https://github.com/affaan-m/ECC) · [Skill Doc](skills/ecc-workflow/SKILL.md)

---

### obsidian-vault-enhance — Obsidian Note Enhancement

**Purpose** — Automatically enrich Obsidian notes with Dataview queries, Mermaid diagrams, semantic callouts, aliases, Templater templates, and more. Detects note type from its folder and filename prefix (HCIP / HCIA / RHEL / Index / Python / General), then applies type-specific enhancement suites.

**Usage** — Trigger in Claude Code; the skill follows a 5-phase pipeline:

```
Phase 1: Read note → identify type (by folder + filename prefix)
Phase 2: Understand content → determine applicable enhancements (flow diagrams? config examples?)
Phase 3: Universal enhancements (frontmatter + aliases + fileClass validation)
Phase 4: Type-specific enhancements (abstract callout / exam Q&A / Mermaid topology / Dataview index)
Phase 5: Verification (frontmatter integrity + callouts + broken link check)
```

**Links** — [Skill Doc](skills/obsidian-vault-enhance/SKILL.md) · [Mermaid Template Reference](skills/obsidian-vault-enhance/references/mermaid-templates.md) · [Dataview Query Reference](skills/obsidian-vault-enhance/references/dataview-queries.md)

---

## Repository Contents

```
grown-workflow/
|
|-- README.md               # Methodology essay (three core themes)
|-- CLAUDE.md               # AI collaboration contract (project-level behavior rules)
|-- CONTRIBUTING.md         # Contribution guide and Git conventions
|-- CREDITS.md              # Third-party credits and licenses
|-- LICENSE                 # MIT license
|-- STRUCTURE.md            # Archived structure guide
|
|-- .claude/
|   |-- README.md           # Project description (this document, Chinese)
|   |-- README.en.md        # Project description (English)
|   |-- settings.json       # Claude Code project configuration
|   |-- skills/
|   |   |-- ecc-workflow/           # Curated ECC workflow
|   |   |   |-- SKILL.md            #   Core document
|   |   |   |-- commands/           #   8 command references
|   |   |       |-- ecc-plan.md
|   |   |       |-- tdd.md
|   |   |       |-- ecc-code-review.md
|   |   |       |-- ecc-build-fix.md
|   |   |       |-- ecc-refactor-clean.md
|   |   |       |-- e2e.md
|   |   |       |-- ecc-test-coverage.md
|   |   |       |-- ecc-update-docs.md
|   |   |-- obsidian-vault-enhance/  # Obsidian note enhancement
|   |       |-- SKILL.md             #   Core document
|   |       |-- references/
|   |           |-- mermaid-templates.md # Mermaid diagram templates
|   |           |-- dataview-queries.md  # Dataview query reference
|   |-- rules/
|   |   |-- common/               # Universal coding standards
|   |       |-- coding-style.md
|   |       |-- testing.md
|   |       |-- git-workflow.md
|   |       |-- code-review.md
|   |       |-- security.md
|   |       |-- performance.md
|   |       |-- patterns.md
|   |       |-- hooks.md
|   |       |-- agents.md
|   |       |-- development-workflow.md
|   |-- scripts/                   # Project scripts (placeholder)
|
|-- docs/
    |-- README.md              # Archived docs/ guide
    |-- principles.md          # Philosophical principles (Chinese)
    |-- methodology.md         # Skill curation methodology (Chinese)
    |-- plans/
    |   |-- README.md          # plans/ guide
    |   |-- ...plan.md         # Planning records
    |-- sdd/
    |   |-- README.md          # sdd/ guide
    |   |-- ...                # SDD process records
    |-- superpowers/
        |-- README.md          # superpowers/ guide
```

---

## Getting Started

```bash
# Verify ECC plugin is enabled (configured in `.claude/settings.json`)
cat .claude/settings.json

# Not sure which command to start with? Check the scenario table:
cat .claude/skills/ecc-workflow/SKILL.md | grep "| Your scenario" -A 20

# Read CLAUDE.md for project conventions
cat CLAUDE.md
```

---

> This project follows the evolutionary path of *scaffolding before start, progress alternating with normalization, tools growing from pain points*. See [`README.md`](../README.md) for the full story.
