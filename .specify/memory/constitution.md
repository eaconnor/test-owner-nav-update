# Constitution — Test Repo

Trimmed on purpose. Gate rubric only — no org-wide baggage carried over from the real constitution.

## Gates

- **Gate 1 — Understanding.** Do we understand the problem? Checked against ux.md's Acceptance Criteria.
- **Gate 2 — Right Thing.** Does this advance the vision? Checked against vision.md's Acceptance Criteria.
- **Gate 3 — Right Build.** Is it usable and accessible? Checked against design.md's Acceptance Criteria.

A spec does not move to "Ready to Build" without all three gates showing PASS, or an explicit override logged in vision.md's Decision Log.

## Enforcement

`./check-gates.sh` reads the Acceptance Criteria checkboxes in `ux.md`, `vision.md`, and `design.md` directly and exits non-zero if any gate has unchecked boxes. No file, no pass, no proceeding.

It is wired in mechanically, by this chain — all four links are required:

1. `.specify/extensions.yml` registers `check-gates` under `hooks.before_plan`, `hooks.before_tasks`, and `hooks.before_implement` with `optional: false`.
2. Each `speckit-*` skill reads `.specify/extensions.yml` in its Pre-Execution Checks and is instructed to `EXECUTE_COMMAND` every mandatory hook and wait for the result before continuing.
3. `/check-gates` (`.claude/skills/check-gates/SKILL.md`) runs the script from the repo root and hard-stops on a non-zero exit.
4. A resolvable feature context must exist — `.specify/feature.json` or `SPECIFY_FEATURE_DIRECTORY`. Without it `setup-plan.sh` exits 1 and `/speckit-plan` dies at step 1 of its Outline, before it ever reads this constitution. A gate that is never reached is not a gate.

Hooks here carry no `condition:` field on purpose. The skills are instructed to skip any hook declaring a non-empty condition and defer to a HookExecutor that does not exist in this project, so a condition would silently disable the gate.

**What this section used to say, and why it was wrong:** it claimed "enforcement is mechanical, not a norm" while the only thing connecting the script to the workflow was this sentence. Nothing in the `speckit-*` machinery referenced `check-gates.sh` — verified by grep, 2026-09-11 — so enforcement depended entirely on an agent reading this file and choosing to act on it. That is a norm wearing a mechanism's hat. The chain above is the fix.

The only ways past a red gate: checked boxes, or an override logged in `vision.md`'s Decision Log by a human.

## No Giant Repo Rule

Every file here is small and networked, not a dump. If a section grows past a screen, it should become a linked mini-doc instead.
