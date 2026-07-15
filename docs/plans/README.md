# Plans

This directory contains dated implementation plans.

## Rules

- Use plans for non-trivial changes, architectural work, or any change where a
  zero-context engineer would otherwise need to rediscover the approach.
- Prefer filenames like `YYYY-MM-DD-short-name-plan.md`.
- Plans should cite exact spec sections when they exist.
- Plans should stay current enough to reflect what is being implemented.
- Completed plans should retain their verification and review notes as history.
- Prefer over-prescriptive plans on risky work: invariants, hidden couplings,
  rollback, rollout, and anti-mocking guidance should be explicit.
- Do not start risky implementation work until the hardening checklist is
  satisfied and the rollback or sequencing story is written clearly enough to
  survive review.

## Standard

Every plan should include:

- goal
- source documents
- context and key files
- invariants and constraints
- dependency-ordered tasks
- testing plan
- verification and gates
- independent review loop
- out of scope
- fresh-eyes review

For risky changes, also include the plan-hardening material documented in:

- `docs/agent-context/runbooks/hardening-plans.md`

Risky plans are blocked if they do not make explicit:

- what must not change
- enough current-structure context to find the right edit point
- what must stay real in tests
- rollback or rollout sequencing when compatibility depends on it

## Status Index

| Plan | Status |
|------|--------|
| 2026-04-07-bootstrap-scaffold-plan.md | completed — exemplar (bootstrap onboarding example) |
| 2026-04-07-development-documentation-foundation-plan.md | completed — exemplar (operating-model foundation) |
| 2026-04-07-plan-hardening-guidance-plan.md | completed — exemplar (hardening example) |
| 2026-04-07-review-skills-bootstrap-plan.md | completed — exemplar (review-loop example) |
| 2026-04-07-specs-index-renumbering-plan.md | completed |
| 2026-07-14-coalescing-layer-plan.md | active |
| 2026-07-14-external-skill-suites-plan.md | active |
| 2026-07-14-task-class-matrix-plan.md | active — task-class matrix promoted |
| 2026-07-14-call-agent-skill-plan.md | active — call-agent skill promoted after +P review |
| 2026-07-14-propagate-guidance-skill-plan.md | active — skill promoted after +P review |
| 2026-07-14-agent-facing-interfaces-runbook-plan.md | active — first [DOM-14] fold-up (from mm) |
| 2026-07-15-coalescing-method-refinements-plan.md | completed — Class 5+P; six skill refinements landed; [DOM-14] trigger bullet promoted, verification/decay bullets held skill-only per grok review |

## Retired Plans

One line per retired plan; the body lives in git at the source SHA.

| Plan | Dates | Outcome | Absorbed into | Source SHA |
|------|-------|---------|---------------|------------|
