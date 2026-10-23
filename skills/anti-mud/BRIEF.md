# Common brief for parallel agents or sessions

Copy to `docs/agents/cleanup/brief.md`, fill the `<...>`, and give each
agent this file plus its own file list. Keep the agent's own prompt to:
who it is, its branch, its progress file, its files, its job.

```md
# <Workstream> — rules every agent follows

- Plan: <plan file>, read only "<conventions>" and "<your section>".
  File paths and line numbers there may be stale: find things by name.
- Base: fresh from <main branch> (`fetch`, then branch from it). Never
  build on whatever the workspace happened to start at.
- Stay inside your file list. Others own the rest at the same time.
  A shared file you must change: minimal, backwards-compatible, tested,
  named in the PR.
- Before adding anything: search for an existing definition.
- Logic found in the wrong layer moves to its place, with a test.
- Ratchets in CI: <list + today's values>. Never raise one. Lower each
  you improve, measured after rebasing on the latest <main branch>.
- Verify behaviour: <how to run it; what to screenshot, at which sizes
  and themes>; compare before/after yourself; say what differs.
- Shared resources (<local server, ports, DB>): take <lock> before use,
  release it after, never hold it while coding.
- Checkpoint after each logical step: commit (WIP ok), push, update
  <progress file> (done / next / gotchas / where the work is). If told to
  pause: checkpoint and stop.
- Before the PR: rebase, squash WIP into clean commits, rerun every check.
- PR: <title/body rules>; list what changed, what moved to its layer,
  ceilings lowered, verification, anything skipped or crossed. Wait for
  CI green. Do not merge. Final report: short.
```

Coordinator duties are in REMEDIATE.md, "Execute".
