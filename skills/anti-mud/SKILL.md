---
name: anti-mud
description: Learns what a project is meant to be (stack, architecture, boundaries), writes that down, and makes the code stay that way through checks that fail in CI; judges the codebase (new, healthy, drifting, muddy) and acts on it, from choosing an architecture to a wave-by-wave clean-up. Language- and stack-agnostic. Use when adopting or starting a repo, when the user mentions tech debt, ball of mud, drift, duplication, architecture or "keep it clean", before landing a change that adds modules, helpers or layers, or when asked whether a codebase is in good shape.
---

# Anti-mud

A codebase stays clean when its architecture is **written down** and
**enforced by checks**, not when someone remembers it. A long session
forgets; CI does not. So: understand the project, write its architecture,
turn each rule into a check, and judge work against it.

There is no single right architecture. Judge a project against its own
declared design and its ecosystem's conventions, never against a
favourite layout.

## Router

Always run phase 1 first (skip it only if `docs/agents/architecture.md`
exists and still matches the code), then phase 2, then the verdict's file.

| Phase | File |
| --- | --- |
| 1. Understand: explore, ask, write the architecture | [UNDERSTAND.md](UNDERSTAND.md) |
| 2. Assess: measure, verdict | [ASSESS.md](ASSESS.md) |
| 3a. Verdict **new**: choose the architecture | [NEW.md](NEW.md) |
| 3b. Verdict **healthy** or **drifting** | [HEALTHY.md](HEALTHY.md) |
| 3c. Verdict **muddy**: clean-up in waves | [REMEDIATE.md](REMEDIATE.md) |
| 4. Guard: rules into checks; review a change | [GUARD.md](GUARD.md) |

Asked only to review a change? Load the architecture, then go to GUARD.md
step "Review a change".

## What it writes in the project

- The instructions file the tools read every turn (`AGENTS.md`,
  `CLAUDE.md`, ...): a short rules block and the pointer
  "Architecture: docs/agents/architecture.md". Nothing else at the root.
- `docs/agents/architecture.md`: the architecture description and the
  rule → check table (template in UNDERSTAND.md).
- `docs/agents/cleanup/`: plan and state of a muddy-repo clean-up;
  deleted when it ends.

## Skills it calls (the user never has to)

- `improve-codebase-architecture`: phase 1 borrows its friction lens in
  the same walk (no second exploration); the skill itself is called only
  to design the fix for a chosen candidate (its grilling loop), from
  HEALTHY.md or REMEDIATE.md. Hand it the candidate, its friction notes
  and architecture.md, and say to skip its own exploration and go
  straight to the grilling loop: the walk is already done.
  Not installed? The friction lens in UNDERSTAND.md stands on its own;
  for the design step offer `npx skills add mattpocock/skills -g -s
  improve-codebase-architecture`, or design the fix with the user inline.

Reviewing a change stays inline and cheap (GUARD.md); `code-review` only
when the user asks for a deeper pass.

## Principles

Design and testing principles it applies when judging and when writing
code: [PRINCIPLES.md](PRINCIPLES.md). In short:

1. One definition per thing: search before you write.
2. Respect the declared boundaries: dependencies point the way the
   architecture says.
3. A rule without a check erodes; a check outside CI is not a check.
4. Ratchets only go down.
5. Accepted noise hides the next real problem: fix it or ticket it.
6. Mechanical rules belong to machines.
7. Refer to code by name, not by file:line.
8. Stay inside the scope; name what you crossed.
9. Every test has a purpose and can fail; coverage is not a goal.
10. Verify behaviour by running the thing, not only the tests.

## Rules for the skill itself

- Recommend, don't impose: options with trade-offs, the user decides.
- Ask when the intent is unclear; never guess an architecture into law.
- Evidence with every verdict: numbers and named places, not adjectives.
- No file-length or line-count limits: they split code arbitrarily.
