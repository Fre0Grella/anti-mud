# Phase 2: assess

Measure the same signals every time, so a later run shows a trend.

## Signals

| Signal | How |
| --- | --- |
| Duplication % | the stack's copy-paste detector, tests excluded |
| Linter warnings | count with the project's own config |
| Boundary breaches | imports that break the dependency rules |
| Cycles | dependency cycles between modules or groups |
| Dead code | unused files, exports, dependencies |
| Type coverage | which kinds of source are typechecked, and errors |
| Rules in the wrong place | domain rules sitting in views, handlers, scripts (sample) |
| Many copies of one thing | the same constant, asset or helper defined twice+ |
| Tests | do the core rules have purposeful tests? (PRINCIPLES.md) |
| Guards | which rules in architecture.md have a check in CI |

Then fold in the friction notes from phase 1 (no second walk of the
code): run the deletion test on each suspect and keep the ones that
earn a place in the report, named with those terms (module, interface,
depth, seam, locality).

## Verdict

- **New:** little code yet, or no architecture to speak of. → NEW.md
- **Healthy:** signals low for the size and ecosystem, boundaries
  respected, and the important rules have checks in CI. → HEALTHY.md
- **Drifting:** mostly sound, but breaches, copies or missing guards are
  accumulating in places. → HEALTHY.md (drifting section)
- **Muddy:** boundaries unclear or widely broken, many copies of one
  thing, rules spread through views, changes ripple. → REMEDIATE.md

Clean but unguarded is not healthy: it is drifting-to-be. Say so.

## Report

Lead with the verdict, then the evidence: each signal with its number,
the worst three places by name, what is guarded and what is not.
