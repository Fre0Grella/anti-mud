# anti-mud

An agent skill that keeps a codebase, in any language, from turning into
a ball of mud.

A long coding session forgets; CI does not. So instead of a list of good
intentions, anti-mud learns what the project is meant to be, writes that
down, and turns each architectural rule into a check that fails in CI.

## What it does

1. **Understand.** Explores the stack, the ecosystem's conventions, the
   structure and the written intent; asks what the code can't answer;
   writes `docs/agents/architecture.md` with a rule → check table.
2. **Assess.** Measures the same signals every run, package by package
   (duplication, one concept with many implementations, styling outside
   the design system, warnings, boundary breaches, cycles, dead code,
   type coverage, test purpose, guards) and gives a verdict with evidence: **new**,
   **healthy**, **drifting** or **muddy**.
3. **Act on the verdict.**
   - *New:* helps choose an architecture from the ecosystem's
     conventions; installs the guards on day one.
   - *Healthy:* says so, with numbers; offers missing guards or asks
     what to improve.
   - *Drifting:* guards first, then the worst places.
   - *Muddy:* maps the mud and pays it down in waves (guards, parallel
     workstreams, structure, edges), with continuous checkpoints.
4. **Guard.** Each rule becomes a ratchet that only goes down (import
   rules for layering, a duplication threshold, max warnings, dead-code
   and type checks), plus a lightweight review of changes against the
   architecture.

No favourite layout: a project is judged against its own declared
design and its ecosystem's standards.

## Install

With the [skills CLI](https://github.com/vercel-labs/skills) (Claude
Code, Codex, Cursor and other agents):

```sh
npx skills add Fre0Grella/anti-mud -g
```

As a Claude Code plugin:

```text
/plugin marketplace add Fre0Grella/anti-mud
/plugin install anti-mud@anti-mud
```

Update later with `npx skills update` or `/plugin marketplace update anti-mud`.

### Recommended companion

anti-mud borrows the friction lens of Matt Pocock's
`improve-codebase-architecture` and calls it to design structural fixes.
It works without it, but better with it:

```sh
npx skills add mattpocock/skills -g -s improve-codebase-architecture
```

## Use

Ask your agent things like "is this codebase in good shape?", "set up
anti-mud guards for this repo", "this is a ball of mud, help me clean
it up", or "review this change against the architecture". It also
triggers on its own when you start a repo or add modules and layers.

## Files it writes in your project

- A short rules block in your agent-instructions file (`AGENTS.md`,
  `CLAUDE.md`, ...) pointing at the architecture file.
- `docs/agents/architecture.md`: the architecture and the rule → check
  table.
- `docs/agents/cleanup/`: plan and progress of a clean-up, deleted when
  it ends.

## License

MIT
