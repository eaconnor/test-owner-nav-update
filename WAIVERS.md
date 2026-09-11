# WAIVERS.md — the override ledger

**Gates here do not stop work. They require a signature.**

Any gate, check or never event can be bypassed. What cannot happen is bypassing one *silently*. A waiver records who proceeded, past what, why, and **what they predicted it would cost if they were wrong** — settled later against what it actually cost. Read by `./check-waivers.sh`.

## Why it works this way

A gate that idles an engineer for six weeks gets removed, and it deserves to be. Design and engineering must be able to work on other things while research runs. The problem was never people proceeding — it was proceeding **without knowing what they were accepting**, and nobody being able to tell afterwards whether the gate was right.

**Non-blocking is about people, not actions.** A pending signature never idles anyone; they move to other work. What waits is the risky action, or shipping it to that destination.

**Calibration is the point.** `VINDICATED` waivers are evidence a gate is too strict. `COSTLY` ones are evidence it was right. A gate whose authority comes from evidence outranks one whose authority comes from policy. **A waiver is not a failure** — if none are ever vindicated, the gates are theatre.

## Who signs — tiered by consequence, not by rank

Run `python3 scripts/check-tier.py` for the live assignment.

| tier | consequence lands on | signs |
|---|---|---|
| `T0` | the person doing the work | themselves (self-serve) |
| `T1` | the team or the roadmap | one peer, not the author |
| `T2` | a **user** | the accountable owner. **Not self-signable by the builder** |
| `T3` | the **company** (legal/regulatory) | accountable owner + risk function, two named signatures |
| `T4` | unbounded or irreversible | **nobody.** A never event is an incident, not a waiver |

Notification threshold is **T2 and above**. A T0 waiver that pings a channel has been silently upgraded to T2, and the engineer will notice before you do.

## Status values

`PENDING` proceeded, outcome unknown · `VINDICATED` bypass was fine, gate may be too strict · `COSTLY` it bit, gate was right · `FATAL` caused a never event or shipped harm — investigate, do not score

## Waivers

| id | date | who | bypassed | why | risk accepted | predicted cost | actual cost | status |
|---|---|---|---|---|---|---|---|---|
| W-01 | 2026-09-11 | Beth Connor | `spec.md` template shape | Hand-wrote the spec as What / Why / Open Questions instead of the `spec-template.md` shape | A spec no `/speckit-*` command can read | Rework if the speckit lifecycle is ever used on this repo | Not yet known — recorded as OPEN.md H-01 rather than fixed silently | `PENDING` |
| W-02 | 2026-09-11 | Beth Connor | intent spec | Proceeded with gate criteria that trace to no canonical document | Criteria nothing can validate; `check-trace.sh` exits 5 | Criteria drift undetected | Not yet known — OPEN.md H-02 | `PENDING` |
| W-03 | 2026-09-11 | Claude | "write it down and it will be followed" | Assumed documented rules change behaviour | That documentation alone would be read and obeyed | Assumed near-zero | **Zero behaviour change, measured** — 12 agents, 6 controlled pairs, 6 ties. See VALUE.md V-04 | `COSTLY` |

## Counts

Computed, never asserted — run `./check-waivers.sh`.
