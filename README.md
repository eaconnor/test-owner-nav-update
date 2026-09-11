# Spec-driven design with gates that actually fire

A working template for wiring **design and research judgement into a spec-kit project** so it survives contact with an engineering workflow. Nine scripts, five registers, one config file.

This repo is the **template**. The worked example — a full pipeline run with red gates, real evidence and real defects — is [test-repo-doodle-journal](https://github.com/eaconnor/test-repo-doodle-journal).

## The finding this is built on

A gate written in prose does not fire.

That is not a hunch. A controlled test ran **12 fresh agents on 6 trap tasks** — half with the 866-line gate documents present, half with them deleted. **Six of six pairs tied.** Not one agent cited either document. One agent put an emoji in the markup while holding the file that bans emoji; another built a confirmation dialog while holding the section stating that discard must never be confirmed.

The same rules, moved into scripts, then found: 10 live accessibility violations in a build two critic passes had cleared, 5 requirements tracing to no stated intent, 2 gate boxes ticked while false, a cited claim contradicted by its own primary source, and a sequencing error in the register itself.

**Rules belong in the execution path. Everything else is a reading assignment nobody does.**

## Setup

```bash
cp project.conf.example project.conf   # or edit project.conf directly
```

`project.conf` is the only project-specific file. Design tokens are read from your build's own `:root` block — **there is no palette hardcoded in any script**, so this works with Apex or any other design system. Hazards come from `HAZARDS.md`, criteria from the gate files, the accountable owner from the config.

```bash
./check-gates.sh && ./check-eng.sh && python3 scripts/check-risk.py internal-demo
```

## The scripts

| script | question | exit |
|---|---|---|
| `./check-gates.sh` | are the gate boxes ticked? | 1 open · **fails on zero parsable criteria** |
| `./check-blocked.sh` | are we waiting on a *person*? | 2 if a HUMAN row stands |
| `./check-trace.sh` | have criteria drifted from what they claim to enforce? | 4 broken trace · 5 no intent spec |
| `scripts/check-design.py` | does the **build** obey the design system? | 6 violation · 7 unresolved · 5 no build |
| `scripts/check-risk.py <dest>` | risk of shipping **to a named destination**? | 9 ship-blocking · 2 no destination given |
| `./check-eng.sh` | the five gates eng owns | 10 can harm a user · 11 off-roadmap · **12 unevaluated** |
| `./check-never.sh` | has something happened that never should? | 20 — stop and investigate, do not score |
| `./check-value.sh` | is the contribution register honest? | 13 if it records no costs |
| `./check-waivers.sh` | are the gates worth obeying? | 15 never event waived · 16 undeclared bypass |
| `scripts/check-tier.py` | who signs to proceed? | 17 if the tiering is a bottleneck |
| `scripts/ux-score.py` | conformance baseline, ceiling, work list | 0 — reports, never blocks |

**Every exit code is distinct on purpose.** A single pass/fail collapses "a box is unticked", "a person owes us an answer", "a criterion points at nothing" and "this build can hurt someone" into one number, losing the only information that tells you what to do next.

**Zero findings is never a pass.** Three scripts fail when they can parse nothing, because "I found nothing" must never render as "nothing is wrong". That false green is the failure this repo documents — and it happened twice while building it.

## Gates do not block work

Engineering and design must be able to work on other things while research runs. A gate that idles people for six weeks gets removed, deservedly. So:

- **Gate 3 splits into FLOOR and FIT.** FLOOR — accessibility, data integrity, lawfulness, security — is never gated on problem validation. You do not wait for a reaction test to label a form field. FIT is polish that only pays off if the concept survives. `check-eng.sh` separates them; only FIT waits.
- **Anything can be bypassed, nothing silently.** `WAIVERS.md` records who proceeded, past what, and the **predicted** cost if wrong — settled later against the actual. `VINDICATED` waivers are evidence a gate is too strict; `COSTLY` ones are evidence it was right. A gate whose authority comes from evidence outranks one whose authority comes from policy.
- **Signatures are tiered by consequence, not rank.** T0 self-serve → T1 a peer → T2 the accountable owner (a user bears it) → T3 owner + risk function (the company bears it) → T4 nobody, it is an incident. Escalating by rank is what makes sign-off hated; escalating by who gets hurt is defensible.
- **Non-blocking is about people, not actions.** A pending signature never idles anyone. What waits is the risky action, or shipping it to that destination.

## The registers

| file | holds | integrity rule |
|---|---|---|
| `OPEN.md` | every unresolved thing, typed `HUMAN` / `RESEARCH` / `ACCEPTED` | `blocks` means "cannot be settled until you decide", never "is relevant to" |
| `HAZARDS.md` | what goes wrong, to whom, per destination | every row names a real source; criticals never average away |
| `VALUE.md` | what research and design actually contributed | **fails if it records no costs** — a register of only wins is a case study |
| `WAIVERS.md` | who bypassed what, and what it cost | every waiver names the risk it accepted |
| `instruments/` | the protocols that would settle the human-gated criteria | thresholds declared **before** any data exists |

The `HUMAN` / `RESEARCH` distinction is load-bearing: a `HUMAN` row is a decision no amount of research resolves, and an agent that guesses past one has made the exact error the register exists to prevent.

## Known rough edges in this repo

Recorded rather than hidden, and each has an `OPEN.md` row:

- `spec.md` is hand-written as *What / Why / Open Questions* — a shape no `/speckit-*` command recognises (H-01)
- `plan.md` and `tasks.md` are stubs of the kind `/speckit-plan` generates (H-01)
- There is **no intent spec**, so `check-trace.sh` exits 5 and no `traces_to:` can be validated (H-02)
- All 10 criteria here are ticked, so `check-gates.sh` exits 0. A template whose gates are green teaches nothing about red ones — see the worked example for that (H-03)
- There is no build, so `check-design.py` exits 5 and `check-eng.sh` exits **12 — unevaluated, not passing** (A-01)
- Criteria here are settled by reading, not by a command, so `check-eng.sh` EG-4 correctly reports a low executable count

## What's ours and what isn't

`.specify/` and `.claude/skills/speckit-*` are **vendored from [github/spec-kit](https://github.com/github/spec-kit)**. They are committed rather than gitignored on purpose: the `speckit-*` skills are the layer that reads `.specify/extensions.yml`, so enforcement only travels with the repo if they do. Everything else — the scripts, the registers, the gate files — is original. MIT licensed; fork it, teach it, build on it.
