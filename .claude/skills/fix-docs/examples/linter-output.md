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

## `vale` output (`just lint-prose`)

```text
 docs/CONCEPT.md
 12:1   warning  'Key Design Decisions' should   little-matches.Headings
                 use sentence-style
                 capitalization.
 45:15  error    Did you really mean             Vale.Spelling
                 'metareasoning'?
 78:5   warning  'in order to' is too wordy.     write-good.TooWordy

 docs/design/overview.md
 3:20   error    AI hedge: 'it is important to   ai-tells.HedgingPhrases
                 note that'. Delete this
                 throat-clearing and state your
                 point directly.
 15:8   error    Did you really mean             Vale.Spelling
                 'skeuomorphic'?
 22:12  warning  'due to the fact that' is too   write-good.TooWordy
                 wordy.
```

Each finding shows `line:col severity message rule`. Findings are grouped by file.

Severity levels: `error`, `warning`, `suggestion`.

Use the rule name to categorize:

- `Vale.Spelling` or `Google.Spelling` = vocabulary finding (add the word to the accept list)
- `little-matches.Headings`, `write-good.*`, `Google.*`, `proselint.*`, `ai-tells.*` = prose style finding
