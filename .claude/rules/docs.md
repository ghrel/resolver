---
paths:
  - "**/*.md"
---

# Conventions for Markdown files

## Linting

All Markdown files must pass both `rumdl` and `vale` with zero warnings and errors.

**Fixing lint issues:** run `just lint-docs` to check all docs, or use `/fix-docs` to run linters and fix findings in a loop until clean.

**Just recipes:**

| Recipe | What it runs |
|---|---|
| `just lint-docs [files]` | All doc linting (markdown + prose) |
| `just lint-markdown [files]` | `uvx rumdl check` |
| `just lint-prose [files]` | `uvx vale` (human-readable) |

All recipes default to `.` (whole project) when called without file arguments.

**No unilateral suppressions:** never add file-level or global suppressions for `rumdl` or `vale` without asking the user first. To add project-specific vocabulary for `vale`, add entries to `.vale/config/vocabularies/little-matches/accept.txt` in alphabetical order.

## Conventions

- Use ATX-style headings, dash list markers, and backtick code fences
- Use `/fix-docs` to run linters and fix findings in a loop
