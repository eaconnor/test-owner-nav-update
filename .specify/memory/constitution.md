# Constitution — Test Repo

Trimmed on purpose. Gate rubric only — no org-wide baggage carried over from the real constitution.

## Gates

- **Gate 1 — Understanding.** Do we understand the problem? Checked against ux.md's Acceptance Criteria.
- **Gate 2 — Right Thing.** Does this advance the vision? Checked against vision.md's Acceptance Criteria.
- **Gate 3 — Right Build.** Is it usable and accessible? Checked against design.md's Acceptance Criteria.

A spec does not move to "Ready to Build" without all three gates showing PASS, or an explicit override logged in vision.md's Decision Log.

Enforcement is mechanical, not a norm: run `./check-gates.sh` before `/speckit-plan` or `/speckit-implement`. It reads the Acceptance Criteria checkboxes in ux.md, vision.md, and design.md directly and exits non-zero if any gate has unchecked boxes. No file, no pass, no proceeding.

## No Giant Repo Rule

Every file here is small and networked, not a dump. If a section grows past a screen, it should become a linked mini-doc instead.
