# Verdict muddy: clean-up in waves

A muddy repo is not fixed in one PR. Plan it, then pay it down in waves,
each one merged and green before the next depends on it.

## 1. Map the mud

From the assessment, list each problem, package by package, with its
size and places: "logo drawn 7 ways", "3 request wrappers", "domain rules
in 12 views", "store doing 10 jobs". Every concept-table row with two
or more copies and every module with rules tangled with I/O is a
problem on this list; each lands in a workstream or is set aside with a
reason. Group them into workstreams that touch disjoint files; every
package with findings gets one.

## 2. Write the plan

`docs/agents/cleanup/plan.md`: conventions every worker follows, then the
waves. The usual order:

- **Wave 0, guards:** every ratchet at today's value, in CI, proven to
  fail. Nothing gets worse from here on. Also root clean-up (dead files).
- **Wave 1, independent workstreams in parallel:** each a domain area or
  a duplicated concern (one client, one brand source, one rule module).
- **Wave 2, structure:** the shared state and the folder layout, after
  wave 1 so the moves don't collide. Update path-based checks and re-prove
  them after any move.
- **Wave 3, the edges:** shared UI or interface primitives first, then
  each screen/endpoint group in parallel on top of them.

Each wave lowers the ratchets it improves. A structural workstream
(deepening a module, moving a seam) is designed first by calling
`improve-codebase-architecture` on that candidate (see SKILL.md, "Skills
it calls"), then planned. Show the user the plan before starting; their
decisions go into the plan file.

## 3. Execute

- One branch and PR per workstream; one owner per file.
- Parallel workers get the common brief: [BRIEF.md](BRIEF.md).
- **Checkpoint continuously:** each worker commits, pushes and updates
  `docs/agents/cleanup/progress-<name>.md` (done / next / gotchas / where
  the work is) after every logical step. A limit or crash must cost
  nothing; "continue" must be enough to resume.
- `docs/agents/cleanup/resume.md` (coordinator): state of every wave,
  worker ids and branches, owner decisions, open questions, the exact
  resume message per worker. An open question is not a yes: wait.
- Review each PR (GUARD.md, "Review a change"), comparing behaviour with
  the old code (same messages, timings, order of side effects), then merge.
  After each merge tell the remaining workers main moved and the new
  ceilings.

## 4. Close

Re-run the assessment, report before → after for every signal, delete
`docs/agents/cleanup/`, keep architecture.md current.
