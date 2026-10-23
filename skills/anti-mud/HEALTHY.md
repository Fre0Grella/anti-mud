# Verdict healthy or drifting

## Healthy

Say so plainly, with the numbers from the assessment, so the team knows
the project is in good shape. Then:

- Any important rule without a check: offer to add it (GUARD.md).
- Nothing missing: ask what they would like better. Do not invent work.

## Drifting

A small, ordered plan; usually one or two PRs:

1. Add the missing guards at today's values first, so it stops getting
   worse while you fix it.
2. Fix the worst places by name (merge the copies, move rules to their
   layer, cut the breaches), lowering each ratchet as it improves. For a
   structural candidate (a shallow module, a leaking seam), call
   `improve-codebase-architecture` on that candidate to design the fix.
3. Re-run the assessment and report the new numbers.

If the drift turns out wide, it is muddy: go to REMEDIATE.md.
