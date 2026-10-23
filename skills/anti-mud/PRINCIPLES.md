# Principles

Each one: why it erodes over long or repeated sessions, and what holds
it. The examples come from a real clean-up; the principles are not tied
to its stack.

## Design

### 1. One definition per thing: search before you write

**Erodes because** a new session does not know a helper exists, so it
writes another; each copy is reasonable alone, together they disagree.
*Seen: one logo drawn 7 ways, 3 request wrappers, a name helper written
3 times, one limit defined twice.*
**Holds with:** the rules block ("search first"), a duplication ratchet,
and merging any second copy you find in the same change.

### 2. Respect the declared boundaries

**Erodes because** the quickest place for new logic is the file you have
open, whatever layer it is in. Soon the rule exists only there, can't be
reused, and can't be tested on its own.
What "the right place" is depends on the project's own architecture
(layers, features, packages, ports and adapters) and its ecosystem; read
architecture.md, don't import a favourite layout.
**Holds with:** dependency rules as an import check in CI; moving a rule
to its place always brings a test with it.

### 3. A rule without a check erodes; a check outside CI is not a check

**Erodes because** a rule only written down is forgotten late in a long
session, and a tool run "now and then" stops being run.
*Seen: a template typechecker only run by hand, so its errors were
tolerated for days.*
**Holds with:** the rule → check table; every check in CI the day it is
added.

### 4. Ratchets only go down

**Erodes because** raising a limit "just this once" is easier than
fixing. **Holds with:** limits set to the measured value, lowered in the
PR that improves them, never raised; measured after rebasing.

### 5. Accepted noise hides the next real problem

**Erodes because** "only the known errors" gets repeated until nobody
reads past it. *Seen: five PRs reported "only the known type errors";
one was a real bug.* **Holds with:** each known warning fixed or
ticketed at once; ratchets that make the count visible.

### 6. Mechanical rules belong to machines

**Erodes because** format, naming and commit-message shape slip late in a
session. **Holds with:** hooks and CI checks; templates or scripts for
anything repeated.

### 7. Refer to code by name, not by file:line

**Erodes because** plans outlive the layout they describe. *Seen: after
a folder move every file:line in a plan was wrong.* **Holds with:**
briefs that name things and say "search for it".

### 8. Stay inside the scope; name what you crossed

**Erodes because** a fix next door looks free, and in parallel work it
becomes a merge conflict. **Holds with:** a file list per worker; any
crossing minimal, backwards-compatible, named in the PR.

## Tests

### 9. Every test has a purpose and can fail

A big suite is not a safe one: tests written for coverage make CI slower
and guarantee little.

- **A stated purpose:** each test protects a named rule, behaviour or
  past bug, and its name says which.
- **Through the interface,** not the internals: a refactor keeps it
  green, a behaviour change turns it red.
- **It can fail:** break the code on purpose once and watch it go red.
  A test that cannot fail is CI time with no guarantee.
- **Coverage is a map, not a goal:** it shows what is untested; never
  ratchet it. For a quality number, mutation score says whether the
  tests notice changes.
- **Where the risk is:** domain rules, boundaries, one regression test
  per fixed bug. Not trivial accessors or framework glue.
- **Deterministic and fast:** no sleeps, no order dependence; fakes only
  at real seams (the adapters), not around every call.
- **No duplicates:** two tests asserting the same thing; delete the
  weaker. A test that protects nothing goes too.

### 10. Verify behaviour by running the thing

**Erodes because** green tests feel like done. *Seen: a one-line layout
fix passed every check and wrapped a title onto three lines; only the
screenshot caught it.* **Holds with:** run it as a user would; for UI,
compare before/after at the sizes and themes that matter, and look.
