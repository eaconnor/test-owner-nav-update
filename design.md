---
scope: feature
parent_ux: ux.md
design_system: "(test) Apex-lite"
gate: 3
eval_loop: built-in — see "Acceptance Criteria" below
---

# design.md — (Test) Nav Update

## Rules Pulled From the Design System

- Nav ≤ 2 levels deep. Active state = left border, brand accent color. [CS: UNKNOWN — placeholder token names, confirm against the real system before use]

## Acceptance Criteria — Gate 3: Are we making the thing right?

- [x] WCAG AA contrast pass — [TEST DATA] simulated pass, not a real audit
- [x] Keyboard-navigable, screen-reader labeled — [TEST DATA] simulated pass
- [x] SUS ≥ 6 to ship, ≥ 8 on the top-five tasks named in ux.md — [TEST DATA] simulated score: 7.8 overall, 8.4 on Top Task #1. Beats the 5.2 baseline from ux.md.
- [x] Design-system conformance — agent-checkable, tokens only, no one-off styles — [TEST DATA] simulated pass
