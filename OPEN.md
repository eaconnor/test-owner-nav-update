# OPEN.md — the register of everything unresolved

One index for every open question, riskiest assumption, and accepted risk. **If it is unresolved and it matters, it has a row here.** Read by `./check-blocked.sh`, which is why the table format is strict.

## The kinds — this is the load-bearing distinction

| kind | meaning | who unblocks it | machine behaviour |
|---|---|---|---|
| `HUMAN` | A **decision** only a person can make. No research resolves it. | named owner | **Stop and ask.** Do not infer, do not pick a sensible default, do not proceed "provisionally." |
| `RESEARCH` | **Evidence** is missing. The question has a findable answer nobody has found. | anyone who can do the work | Proceed flagged. May build, must not claim validation. |
| `ACCEPTED` | A known weakness being **deliberately carried**. | already decided | Proceed. Must stay visible; never silently dropped. |

An agent that hits a `HUMAN` row and guesses anyway has made the specific error this file exists to prevent.

**The `blocks` column means "cannot be settled until you decide" — NOT "is relevant to."** Conflating those produces false never events in `check-never.sh` NE-1, and a false never event is how the whole mechanism gets switched off.

## Open rows

| id | kind | question / assumption | owner | blocks | resolves_when |
|---|---|---|---|---|---|
| H-01 | HUMAN | `spec.md` here is hand-written as What / Why / Open Questions — a shape no `/speckit-*` command recognises. `plan.md` and `tasks.md` are two-line stubs that `/speckit-plan` and `/speckit-tasks` would generate. Fix the shape now this repo is public and read as a template, or leave it as a documented rough edge? | Beth Connor | this repo's credibility as a template | Beth says fix or leave |
| H-02 | HUMAN | This repo has **no intent spec**, so `check-trace.sh` exits 5 and no criterion's `traces_to:` can be validated. Author one, or accept that Gate criteria here are unanchored? | Beth Connor | check-trace.sh being able to run at all | An intent spec exists, or the decision is recorded |
| H-03 | HUMAN | All 10 criteria here are ticked and `check-gates.sh` exits 0. A template whose gates are green teaches nothing about red ones. Add a deliberately-open criterion, or point readers at the doodle-journal example for that? | Beth Connor | what a first-time reader learns | Beth picks |
| A-01 | ACCEPTED | There is no build in this repo, so `check-design.py` exits 5 and `check-eng.sh` EG-1 is **UNEVALUATED, not passing**. An unevaluated harm gate must never read as a clear one. | — | nothing; must stay visible | n/a — carried until a build exists |

## Counts

Computed, never asserted — run `./check-blocked.sh`.

## Resolved

Rows move here with a date and an outcome. Nothing is deleted; a register you can rewrite silently is not a record.

| id | kind | outcome | date |
|---|---|---|---|
| H-00 | HUMAN | Repo made public; MIT licence and spec-kit attribution added first. | 2026-09-11 |
