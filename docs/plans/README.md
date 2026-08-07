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
| 2026-04-07-specs-index-renumbering-plan.md | retired-pending — soft-retired 2026-08-07 sweep; source `2415252` |
| 2026-07-14-coalescing-layer-plan.md | active |
| 2026-07-14-external-skill-suites-plan.md | active |
| 2026-07-14-task-class-matrix-plan.md | active — task-class matrix promoted |
| 2026-07-14-call-agent-skill-plan.md | active — call-agent skill promoted after +P review |
| 2026-07-14-propagate-guidance-skill-plan.md | active — skill promoted after +P review |
| 2026-07-14-agent-facing-interfaces-runbook-plan.md | active — first [DOM-14] fold-up (from mm) |
| 2026-07-15-coalescing-method-refinements-plan.md | completed — Class 5+P; six skill refinements landed; [DOM-14] trigger bullet promoted, verification/decay bullets held skill-only per grok review |
| 2026-07-28-guidance-gates-plan.md | retired-pending — soft-retired 2026-08-07 sweep; source `2415252` |
| 2026-07-15-interface-review-skill-promotion-plan.md | retired-pending — soft-retired 2026-08-07 sweep; source `2415252` |
| 2026-07-30-program-theory-and-module-theory.md | active — Class 3+P; landed `4acbad1` pre-review (deviation recorded); independent review 2026-07-30 + repair pass; propagation blocked until repair lands; full [DOM-16] still deferred |
| 2026-08-06-register-conditioning-theory-revision-plan.md | completed — Class 5; two independent reviews (delta + amendment); owner adopted 2026-08-07; [REV-AT-003], the register falsifier, and the crystallize citation tests landed |
| 2026-08-07-simplebroker-backport-wave-plan.md | completed — Class 5+P; backport wave from SimpleBroker pin `a38e6a9`; three plan-review rounds + three pre-landing rounds (codex); OD-1/2/3/4 executed; landed 2026-08-07 |

## Retired Plans

One line per retired plan; the body lives in git at the source SHA.

| Plan | Dates | Outcome | Absorbed into | Source SHA |
|------|-------|---------|---------------|------------|
| 2026-04-07-specs-index-renumbering-plan | 2026-04-07 | Renumbered the specs index into the stable 00/01 scheme | docs/specs/00-specs-index.md and the [DOM-2] taxonomy | `2415252` |
| 2026-07-15-interface-review-skill-promotion-plan | 2026-07-15 | Promoted the interface-review skill at 3 citations per the [DOM-14] promotion tier (grok-reviewed) | skills/interface-review/SKILL.md; promotion record in docs/coalescing.md | `2415252` |
| 2026-07-28-guidance-gates-plan | 2026-07-28 | Landed the corpus self-check gates (check-doc-paths, coalesce-check, bootstrap adaptation layer) | bin/check-doc-paths, bin/coalesce-check, CHANGELOG 2026-08-06 | `2415252` |
