# Test Repo — Nav Update

What this tests: whether vision.md / ux.md / design.md / constitution.md actually wire together the way the deck says they do, using the "easy" use case (nav update) as the toy example. Plain, generic content on purpose — not real ACP data, not canon.

## Reading order

1. `.specify/memory/constitution.md` — the three gates
2. `vision.md` — Gate 2, are we making the right thing
3. `ux.md` — Gate 1, are we solving the right problem
4. `design.md` — Gate 3, are we making the thing right
5. `spec.md` → `plan.md` → `tasks.md` — the build chain, currently blocked on purpose

## What to break

Try making a change to ux.md's Top Tasks and see whether spec.md's [NEEDS CLARIFICATION] actually changes with it. If it doesn't, the wiring's fake.
