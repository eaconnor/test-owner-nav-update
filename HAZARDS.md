# HAZARDS.md — the hazard register, read by `scripts/check-risk.py`

What actually goes wrong, to whom, and how badly. **Not** a criteria count — `ux-score.py` does that. A project can be 90% conformant and carry a critical hazard, because conformance is measured against what you thought to write down and hazards are not.

`exposure` is per-destination and that is the load-bearing column. A hazard can have exposure **0** at an internal demo and **1.0** the moment a real person is involved. One number for "risk" is a number waiting to be quoted in the wrong room.

`severity`: 1 annoying · 2 harmful · 3 serious · 4 critical. **Any severity-4 hazard with non-zero exposure is ship-blocking regardless of the aggregate** — criticals do not average away.

`floor` marks hazards that hold whether or not the concept is right (accessibility, lawfulness, data integrity). FLOOR is never gated on problem validation.

**Every row must name a real source.** A hypothetical hazard belongs in a risk workshop, not here. Delete the rows below and write your own — they describe *this* repo, not yours.

## Hazards

| id | kind | severity | floor | exp_demo | exp_pilot | exp_prod | what | source | mitigation |
|---|---|---|---|---|---|---|---|---|---|
| RSK-01 | CLAIM | 2 | fit | 0.7 | 0.7 | 0.7 | This repo is read as a finished template and copied wholesale, including its rough edges — a hand-written spec.md shape no speckit command recognises, and stub plan/tasks files. | README "known rough edges"; OPEN.md H-01. | Say so in the README above the fold, and point readers at the worked example instead. Partially mitigated; the residual risk is someone cloning without reading. |
| RSK-02 | EXCLUSION | 3 | FLOOR | 0.0 | 1.0 | 1.0 | No build exists, so no accessibility check has run. EG-1 is UNEVALUATED. The first artifact added here ships with zero accessibility verification unless someone sets BUILD in project.conf. | OPEN.md A-01; `python3 scripts/check-design.py` exits 5. | Set BUILD in project.conf the moment an artifact exists. An unevaluated harm gate must not read as a clear one. |
