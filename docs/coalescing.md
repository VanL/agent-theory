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

## First-Sweep Policy (this repo — executed 2026-07-14, see run log)

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
| Lessons | 2026-04-07 | `5927481` |
| Plans | (none — no retirements yet; status index live) | — |
| Promotion | 2026-07-15 interface-review skill (citations: taut `4a129e9`, mm `b6bded5`, mm `15faadc`) | `30c8b04` (pre-promotion HEAD) |
| Fold-up | 2026-07-15 fold-unit trigger denomination (mm `3487ec358`, weft `8382a4d5`) | `5b990ad` (pre-promotion HEAD) |

## Deferral State

A trip is only news when it is new: unchanged counts against this table do
not re-nag; a changed count or a fired reconsideration condition does.

| Tier | Checked through (date, SHA) | Counts at check | Reason deferred | Reconsider when |
|------|------------------------------|-----------------|-----------------|-----------------|
| Lessons | 2026-07-14, first sweep executed | 2 past watermark — under threshold 10 | Not tripped | Count changes |
| Plans | 2026-07-14, `5927481` | 1 (specs-index-renumbering; four others are exemplar) — under threshold 5 | Not tripped | Count changes |
| Promotion | 2026-07-15, interface-review promoted | 3 citations of one theme (taut MCP plan §16.3–§16.4; mm impl/41 RiskEvaluationApi contract; mm external-API/MCP plan §4/§5/§9) — threshold 3 met | Promoted to `skills/interface-review/SKILL.md` per `docs/plans/2026-07-15-interface-review-skill-promotion-plan.md`; not deferred | New distinct citations of another theme accumulate; recount at next sweep |
| Fold-up | 2026-07-15, coalescing-method-refinements amendment landed (grok-reviewed) | 2 accepted (agent-interface principles, 2026-07-14; fold-unit trigger denomination, 2026-07-15); 1 held skill-only (framework-fact expiry) — see `docs/plans/2026-07-15-coalescing-method-refinements-plan.md` §10 | Trigger denomination (mm recalibration `3487ec358` + weft date-cursor failure `8382a4d5`): two independent lineages — graduated into the [DOM-14] trigger bullet and the skill's step 1. Framework-fact expiry: mm is the single incident lineage (fold `127fd437d`, disposition `712ea5440`); weft's check **did run** at a real pin bump (`8382a4d5` commit message; pin bump `57255b83`) but was a true-negative — zero expiries, no disposition path exercised — and review disposed (F2) that a true-negative validates the check, not the phenomenon: **held skill-only** with the three-tier verification bullet (F3), both awaiting a second lineage. Four further refinements landed skill-only by design (examples-are-claims, catch-all check, collision-aware landing, plus the held pair). **Candidate slate registered 2026-07-17 from mm's lifecycle-rollback process hardening** (mm plan `2026-07-17-process-hardening-after-lifecycle-rollback.md`), all at 1 lineage: revision re-gate + reviewed-baseline pin + Revision Log (mm incident; hub Plan Lifecycle carries a pointer-grade caution citing it); findings-at-standing-boundaries-escalate (1 clean lineage — the interface-review disposition practice is noted but flagged shared-ancestry, does not count as second); standing-invariants-registry pattern; deployment-status qualifier axis (ratified locally in mm's plans README). The commit-scope rule was judged at 2 independent lineages (weft benign omnibus, mm harmful omnibus) and landed as a hub lesson | An actual second-repo expiry fold, or a second repo durably installs the expiry disposition path; second independent lineage or explicit owner direction for the 2026-07-17 slate; recount at the next sibling sweep |

## Run Log

One line per run, newest first. Each line is a claim; it must survive a
spot-check against the diff. `checked-deferred` lines are valid runs. Source
SHA names a commit verifiably containing the raw material; the fold commit
may be appended as metadata once it exists.

| Date | Tier(s) | Source SHA | Claim |
|------|---------|------------|-------|
| 2026-07-15 | Promotion | `30c8b04` (pre-promotion HEAD); citations taut `4a129e9` (§16.3 committed; §16.4 working-tree in its authoring session), mm `b6bded5` (RiskEvaluationApi contract), mm `15faadc` (external-API/MCP plan) | [DOM-14] promotion tier tripped at 3 distinct citations of the agent-facing-interface-review theme. Promoted `skills/interface-review/SKILL.md` (procedure wrapping `designing-agent-facing-interfaces.md`: checklist walk, enumerable-gates step, MCP annotation/description verification, file:line evidence bar; findings-table + ratified-judgments + verdict + runbook-feedback output contract). Opus-drafted, grok-reviewed (PASS-with-changes; 8 findings applied, incl. the skill's own teaching example failing its file:line bar — see plan §4). Registered in repository-map §Skills; runbook back-pointer added. No lessons/plans material folded; those watermarks unmoved. |
| 2026-07-15 | Fold-up + promotion | `5b990ad` (pre-promotion HEAD); evidence mm `3487ec358`/`127fd437d`/`5e8fb8ca7`/`c6356186a`/`63f87cadb`/`a9d17383e`, weft `8382a4d5` | Coalescing-method-refinements amendment (Class 5+P, grok-reviewed): six refinements integrated into `skills/coalescing/SKILL.md`; [DOM-14] trigger bullet promoted (fold-unit denomination + declared progress model, F7 tighten); verification and decay bullets **held skill-only** per review F2/F3 (single lineage — weft's expiry check was a true-negative, not a second incident/adaptation). Two drafting-pass evidence errors corrected at review (F1 weft-check-did-run; F4/F5 SHA mis-pins). Weft's run-log recording gap patched in weft same-day. No raw material folded; no lessons/plans watermark moved. |
| 2026-07-14 | Fold-up | mm `9a8d17d55` (contains mm's proposal record and the harvested source) | First role-symmetric fold-up accepted: mm's agent-API design principles (proposed by mm's root-docs retirement sweep) distilled into `runbooks/designing-agent-facing-interfaces.md`, scaffolded via COPIED_FILES. Lineage accounting per `docs/plans/2026-07-14-agent-facing-interfaces-runbook-plan.md` §2: dual-lineage convergence for two principles (meets the 2-independent threshold), single-lineage generalization by explicit owner direction for the rest, one convergence claim withdrawn as shared-ancestry. Raw material: mm's retired `system_api_design.md` (full text at mm `2b0182200`) and its `implementation/53`. |
| 2026-07-14 | Lessons | `5927481` | First sweep (authorized): folded 12 bootstrap-era entries (2026-04-07) into one pointer line — pure dedup, every entry verified already distilled into [DOM-*] sections, Golden Rules 7–8, or runbooks; no new rules, no Golden Rule changes. Kept 2026-07-02 and 2026-07-06 verbatim (age floor; cited by active plan). Watermark advanced to 2026-04-07. Plans/promotion/fold-up untouched per First-Sweep Policy. Backstitch: clean. |
| 2026-07-14 | — (promotion, not a sweep) | `5927481` | [DOM-14] and deltas §5.1–§5.7 promoted per plan task 3: DOM spec gains §14; engineering-principles gains §15; writing-plans gains Plan Lifecycle and Retirement; maintaining-traceability gains the retired-citation form; plans README gains Status Index + Retired Plans; agent-context README and context.index.yaml gain the hot-lessons projection; lessons.md intro notes startup scope. Nothing folded; no watermark advanced. |
| 2026-07-14 | all | — (additive-only; nothing folded) | Checked-deferred with blockers; see Deferral State. Review passes 1–2 dispositions applied: read-only trigger check, source_sha cue model, additive-only-when-uncommitted, plan mutability boundary, deferral state model, multi-signal decay, independent-lineage fold-up. No fold performed; no watermark advanced. |
| 2026-07-14 | — | — | Layer initialized by docs/plans/2026-07-14-coalescing-layer-plan.md. Derived counts at initialization: lessons 14 entries past (no) watermark; plans 5 completed-unretired by file inspection. |
