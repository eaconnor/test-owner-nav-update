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

## What's ours and what isn't

- `.specify/` and `.claude/skills/speckit-*` are **vendored from [github/spec-kit](https://github.com/github/spec-kit)** — not original work here. Committed rather than gitignored on purpose: the `speckit-*` skills are the layer that reads `.specify/extensions.yml`, so the gate enforcement only travels with the repo if they do.
- `.claude/skills/check-gates/`, `check-gates.sh`, the gate files and the constitution are original.
- Licensed MIT — see `LICENSE`.

## Known rough edges

Left in deliberately, as an honest record rather than a polished template:

- `plan.md` and `tasks.md` are two-line stubs. `/speckit-plan` and `/speckit-tasks` generate these — and a hand-stubbed `plan.md` actively makes `setup-plan.sh` skip its own template copy. Don't copy this pattern.
- `spec.md` is hand-written as `What / Why / Open Questions`, a shape no `/speckit-*` command recognizes. The real shape is `.specify/templates/spec-template.md` — prioritized user stories, `FR-###`, `SC-###`. See `test-repo-doodle-journal/spec.md` for a version that matches.
- `.specify/feature.json` is machine-local (gitignored by spec-kit's own rules), so a fresh clone must create it or export `SPECIFY_FEATURE_DIRECTORY=.` before `/speckit-plan` will run at all.
