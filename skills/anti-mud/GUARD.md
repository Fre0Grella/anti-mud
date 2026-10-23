# Phase 4: guard

## Rules into checks (fitness functions)

For each rule in architecture.md, find a check that fails when the rule
breaks, and fill the rule → check table:

| Rule kind | Check |
| --- | --- |
| Dependency direction / layering | import-rule tool with a known-violations baseline |
| One definition per thing | duplication % ratchet |
| No dead code | unused files/exports/deps, today's findings ignored per file |
| Types hold everywhere | typecheck every kind of source file (templates too) |
| Style and smells | linter at max-warnings = today's count |
| Format | formatter check |
| Behaviour | tests and build |

Rules no tool can check stay in the table as "review only"; the review
step below covers them.

Each ratchet: measure today's value, set the limit to exactly that, put
it in CI, comment in the CI file how to lower it, then break it once on
purpose and see it fail. A tool that cannot cap a count usually has an
"only new issues since <commit>" mode: that is a ratchet too.
After any folder move, re-prove path-based rules still match.

Starting points per stack (verify for the version in use):

| Stack | Lint | Duplication | Layers | Dead code |
| --- | --- | --- | --- | --- |
| JS/TS | eslint | jscpd | dependency-cruiser | knip |
| Python | ruff | jscpd, pylint duplicate-code | import-linter | vulture |
| Go | golangci-lint | its dupl linter | its depguard linter | its unused linter |
| JVM | the build's linter | PMD CPD | ArchUnit | compiler warnings |
| Other | the language's linter | jscpd | the stack's import checker | compiler warnings |

Mechanical rules (format, commit message shape): a pre-commit hook or a
CI check, never memory.

## Rules block

In the instructions file read every turn (adapt to the project):

```md
## Architecture

Architecture and the rule → check table: docs/agents/architecture.md.
Read it before adding modules, helpers or layers.

- One definition per asset, rule, constant and helper: search first,
  reuse or extend.
- Dependencies follow the rules in architecture.md.
- CI ratchets the debt (<checks>). Never raise a ceiling or add to a
  baseline; when you pay debt down, lower it in the same PR.
```

## Review a change

Lightweight by design: read the diff yourself, once, against
architecture.md. Don't spawn reviewers or load a review skill; the user
can ask for `code-review` when a change is risky enough to pay for it.

1. Skim for obvious correctness slips: a changed condition, a dropped
   branch, a reordered side effect, a missing await or error path.
2. The architecture pass:
   - every "review only" rule in the table;
   - a definition that already exists elsewhere (search for it);
   - logic placed in the wrong layer for this architecture;
   - new tests: purpose stated, through the interface, can fail
     (PRINCIPLES.md);
   - ceilings: lowered where improved, never raised;
   - behaviour verified by running it, not only by tests.
3. Report findings by severity; offer the fixes.
