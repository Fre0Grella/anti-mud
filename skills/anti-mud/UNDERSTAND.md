# Phase 1: understand what the project should be

Goal: an architecture description the user confirms. Everything later is
judged against it.

## 1. Explore (read, don't judge yet)

- **Stack:** languages, frameworks, package manager, build, deploy
  targets, runtime(s). Several packages or apps? How do they share code?
- **Ecosystem conventions:** what the language/framework expects
  (standard layout, module system, idioms). These are the defaults.
- **Structure:** top-level folders, how modules group (by layer, by
  feature, by package), the import/dependency graph between groups.
  Walk every package, not only the biggest one.
- **Intent in writing:** README, docs, domain glossary (CONTEXT.md or
  similar), existing decision records, the instructions file, comments
  that state rules.
- **Tests:** what is tested, at which level, what is not.
- **Existing guards:** linters, CI steps, hooks, typecheck, thresholds.
- **Friction notes, for phase 2** (same walk, files already open), in the
  vocabulary of `improve-codebase-architecture`'s LANGUAGE.md (module,
  interface, depth, seam, locality):
  - understanding one concept means bouncing between many small modules;
  - shallow modules: interface nearly as complex as the implementation;
  - pure functions pulled out only for tests, the bugs left in the callers;
  - tightly coupled modules leaking across their seams;
  - a module mixing pure rules with I/O (network, storage, DOM, canvas,
    clock): its rules can't be tested or reused without the side effects;
  - areas untested, or hard to test through their interface.
  Mark suspects for the deletion test: delete it in your head; does the
  complexity vanish (pass-through) or spread to every caller (earning it)?

For a large repo, fan the exploration out to read-only search agents and
keep only their conclusions. Give them one brief with two output
sections, **intent** and **friction**, so neither lens gets dropped.

## 2. Infer, then ask

Write down what the code suggests: the style (layered, hexagonal,
feature-sliced, MVC, package-per-concern, services, ...), the core
domain, and the dependency directions that seem intended.

Ask the user, one batch, only what the code does not answer:

- What is the product, and what part of the code is the heart of it?
- Expected lifetime and team size? (A weekend tool needs fewer guards.)
- Which dependency directions must never be broken?
- Where code and the docs disagree: which one is right?
- Conventions they hold that the code doesn't show yet.

If they have no answer, help define it: propose from the ecosystem's
conventions and the project's goals, with options (see NEW.md).

## 3. Write docs/agents/architecture.md

```md
# Architecture

## What this is
<one paragraph: product, the core domain, who uses it>

## Stack
<languages, frameworks, runtime, build, deploy>

## Shape
<style, and the groups/layers with one line each on what lives there>

## Dependency rules
<which group may depend on which; the ones that must never break>

## Conventions
<naming, where tests live, shared primitives to reuse, error handling>

## Rule → check
| Rule | Check that enforces it | In CI? |
| --- | --- | --- |
| <rule> | <tool + config, or "review only"> | <yes/no> |
```

Then add the rules block and pointer to the instructions file (see
GUARD.md, "Rules block"). Show the user the file; it is theirs to correct.
