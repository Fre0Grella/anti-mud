# Phase 2: assess

Measure the same signals every time, so a later run shows a trend.

Measure each package, app or deployable on its own (frontend, backend,
functions, scripts...). A repo-wide number hides the package nobody
opened.

## Signals

| Signal | How |
| --- | --- |
| Duplication % | the stack's copy-paste detector, tests excluded; then read its clone list, not only the % |
| Linter warnings | count with the project's own config |
| Boundary breaches | imports that break the dependency rules |
| Cycles | dependency cycles between modules or groups |
| Dead code | unused files, exports, dependencies |
| Type coverage | which kinds of source are typechecked, and errors |
| Rules in the wrong place | domain rules sitting in views, handlers, scripts (sample) |
| Many copies of one thing | hunt by concept, not by text: one concept with N implementations (below) |
| Styling outside the design system | inline styles, primitives restyled per component (buttons, dialogs), raw colours instead of tokens |

**One concept, N implementations.** A copy-paste detector misses copies
that differ by a name or a branch. For each package, search for the
concepts that tend to multiply and count the implementations:

- config and environment flags read in several places;
- auth and permission guards;
- error → status or error → message mappings;
- input parsing and body reading, codecs, serialisers;
- validation or sanitising of the same data;
- lookups (find X by id, slug, token) repeated per handler;
- the same asset drawn more than once (inline SVG, canvas), not only
  referenced by path;
- bootstrap code repeated per page or entry point (theme, config, auth);
- formatting (money, dates, names) and request wrappers.

Read each tool's findings list too: a flagged file or folder is a lead
for the map of the mud, not noise to note and move past.
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
