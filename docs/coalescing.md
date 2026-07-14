# Coalescing State

Status: Active — [DOM-14] promoted 2026-07-14 by
`docs/plans/2026-07-14-coalescing-layer-plan.md` (promotion in the
worktree; SHA pins when the guidance wave commits).

Owner: any agent that observes a tripped threshold at session start.
Boundary: lessons, plans, and skill/runbook promotion in this repository,
plus cross-repo fold-up (this is the guidance repo). Specs and
implementation docs are living documents and are never coalesced.
Verification: the run log below plus the backstitch self-corpus check.
Required action: the session-start check is **read-only** — derive the
counts, compare against the deferral state below, and report a new trip to
the user in one sentence. All writes to this file or to coalesced material
happen only inside an authorized maintenance task
(`skills/coalescing/SKILL.md`); destructive steps additionally require
landing authorization.

Counts are always derived from watermarks and the current tree — never
stored, never trusted from memory. See the skill for the exact commands.

## Thresholds

| Tier | Trigger (derived count) | Threshold | Age floor |
|------|------------------------|-----------|-----------|
| Lessons | dated ledger entries after the lessons watermark | 10 | 30 days, and never entries cited by an active plan or in a still-accumulating theme |
| Plans | plans with status completed/superseded, not `exemplar`, and no retired-ledger line | 5 | none — the harvest gate and two-step retirement are the guards |
| Promotion | distinct citations of the same workflow theme (judgment-clustered; see skill step 4) since the promotion watermark | 3 | n/a |
| Fold-up (guidance repo only) | sibling-repo golden-rule candidates with independent lineage (not shared bootstrap ancestry) not yet reflected here | 2 independent incidents/adaptations | n/a |

Thresholds are declared here so the trigger check is mechanical, and they
are per-repo values: consumer repos calibrate their own (mm's volume needs
far higher triggers), and the derivation commands must be adapted to each
repo's ledger format. Tuning is legitimate; tune in this file with a
run-log note, not ad hoc.

## First-Sweep Policy (this repo)

- Lessons tier only. The plans tier is **not derivable** until the status
  index from plan §5.5 lands, and stays untouched in the first sweep
  regardless.
- Dedup is mandatory: many 2026-04-07 entries are already distilled into
  Golden Rules — those fold as pointers ("distilled as Golden Rule N"),
  never as duplicate rules.
- The four foundation plans are marked `exemplar` in the proposed status
  index and are exempt from retirement until superseded.
- Destructive steps require landing authorization; an uncommitted first
  sweep is additive-only (drafts and candidates, no deletion, no watermark
  advance).

## Watermarks

| Tier | Distilled through | Source SHA |
|------|-------------------|------------|
| Lessons | (none — first sweep pending) | — |
| Plans | (blocked — no status source until plan §5.5 lands) | — |
| Promotion | (none — first sweep pending) | — |
| Fold-up | 2026-07-02 verification-lessons fold | `5927481` (guidance wave landed 2026-07-14) |

## Deferral State

A trip is only news when it is new: unchanged counts against this table do
not re-nag; a changed count or a fired reconsideration condition does.

| Tier | Checked through (date, SHA) | Counts at check | Reason deferred | Reconsider when |
|------|------------------------------|-----------------|-----------------|-----------------|
| Lessons | 2026-07-14, `5927481` | 14 past (no) watermark — tripped | Sweep is its own unit of work and awaits authorization; raw state now committed, so the destructive phase is unblocked once authorized | User authorizes the first sweep (lessons-only, dedup-first per First-Sweep Policy) |
| Plans | 2026-07-14, `5927481` | 1 (specs-index-renumbering; four others are exemplar) — under threshold 5 | Not tripped | Count changes |
| Promotion | 2026-07-14, `5927481` | not derived (judgment-clustered; done during a sweep) | Derive at first sweep | First sweep runs |
| Fold-up | 2026-07-14, `5927481` | not derived | Provenance pinned; candidates derive at first sweep | First sweep runs |

## Run Log

One line per run, newest first. Each line is a claim; it must survive a
spot-check against the diff. `checked-deferred` lines are valid runs. Source
SHA names a commit verifiably containing the raw material; the fold commit
may be appended as metadata once it exists.

| Date | Tier(s) | Source SHA | Claim |
|------|---------|------------|-------|
| 2026-07-14 | — (promotion, not a sweep) | `5927481` | [DOM-14] and deltas §5.1–§5.7 promoted per plan task 3: DOM spec gains §14; engineering-principles gains §15; writing-plans gains Plan Lifecycle and Retirement; maintaining-traceability gains the retired-citation form; plans README gains Status Index + Retired Plans; agent-context README and context.index.yaml gain the hot-lessons projection; lessons.md intro notes startup scope. Nothing folded; no watermark advanced. |
| 2026-07-14 | all | — (additive-only; nothing folded) | Checked-deferred with blockers; see Deferral State. Review passes 1–2 dispositions applied: read-only trigger check, source_sha cue model, additive-only-when-uncommitted, plan mutability boundary, deferral state model, multi-signal decay, independent-lineage fold-up. No fold performed; no watermark advanced. |
| 2026-07-14 | — | — | Layer initialized by docs/plans/2026-07-14-coalescing-layer-plan.md. Derived counts at initialization: lessons 14 entries past (no) watermark; plans 5 completed-unretired by file inspection. |
