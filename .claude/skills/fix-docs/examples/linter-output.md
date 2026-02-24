# Linter output examples

Sample output from each linter to help with categorization.

## `rumdl` output

```text
docs/CONCEPT.md:15:1: [MD004] Unordered list style: Expected: dash; Actual: asterisk [*]
docs/CONCEPT.md:42:81: [MD009] Trailing whitespace [*]
docs/design/overview.md:1:1: [MD041] First line in a file should be a top-level heading [*]

Issues: Found 3 issues in 2/5 files (12ms)
Run `rumdl fmt` to automatically fix 3 of the 3 issues
```

Each line follows the pattern `file:line:column: [RULE] description [*]`. The `[*]` suffix means the finding supports auto-fix via `rumdl fmt`.

## `vale` summary output (`just lint-prose-summary`)

```text
## 6 findings (2 error, 4 warning)

### By file
    3  docs/CONCEPT.md
    3  docs/design/overview.md

### By rule
    2  write-good.TooWordy
    2  Vale.Spelling
    1  little-matches.Headings
    1  ai-tells.HedgingPhrases

### Spelling (2 words to add to vocabulary)
  metareasoning
  skeuomorphic

### Findings

  docs/CONCEPT.md
    12:1 w little-matches.Headings: 'Key Design Decisions' should use sentence-style capitalization.
    45:15 e Vale.Spelling: Did you really mean 'metareasoning'?
    78:5 w write-good.TooWordy: 'in order to' is too wordy.

  docs/design/overview.md
    3:20 e ai-tells.HedgingPhrases: AI hedge: 'it is important to note that'. Delete this throat-clearing and state your point directly.
    15:8 e Vale.Spelling: Did you really mean 'skeuomorphic'?
    22:12 w write-good.TooWordy: 'due to the fact that' is too wordy.
```

The summary is pre-categorized into sections:

- **By file** — which files need work and how many findings each
- **By rule** — what categories of fixes are needed
- **Spelling** — words to add to the vocabulary accept list (only present when there are spelling findings)
- **Findings** — all findings grouped by file, one line each: `line:col severity rule: message`

Severity codes: `e` = error, `w` = warning, `s` = suggestion.

Use the rule name to categorize:

- `Vale.Spelling` or `Google.Spelling` = vocabulary finding (listed in the Spelling section)
- `little-matches.Headings`, `write-good.*`, `Google.*`, `proselint.*`, `ai-tells.*` = prose style finding

### Filtering

The summary script supports `--file` and `--rule` flags for filtered views:

```bash
# Show only findings for a specific file
uvx vale --output=JSON --no-exit . | python3 tools/vale_summary.py --file CONCEPT.md

# Show only findings for a specific rule
uvx vale --output=JSON --no-exit . | python3 tools/vale_summary.py --rule Spelling
```
