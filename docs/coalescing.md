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
(`skills/coalescing/SKILL.md`). A routine authorized sweep is
plan-exempt and needs no separate landing authorization when every
removal has a verified pre-fold source cue reachable from a retained
ref and no durable guidance is promoted or materially revised
([DOM-5]/[DOM-14] archive rule); worktree-only material remains
ineligible for removal.

Counts are always derived from watermarks and the current tree — never
stored, never trusted from memory. The derivation recipe in
`skills/coalescing/SKILL.md` step 1 and this file's thresholds are one
recipe, and that recipe is authoritative. `bin/coalesce-check` is an
**evidence trail, not a second recipe**: it verifies SHA claims and
retrieval cues and quotes a count, but it is read-only, it never writes
counts back, and when the tool and this file disagree, this file wins
and the script is the defect.

## Thresholds

| Tier | Trigger (derived count) | Threshold | Age floor |
|------|------------------------|-----------|-----------|
| Lessons | dated ledger entries after the lessons watermark | 10 | 30 days, and never entries cited by an active plan or in a still-accumulating theme |
| Plans | plans with status completed/superseded, not `exemplar`, and no retired-ledger line | 5 | none — the harvest gate and two-step retirement are the guards |
| Unindexed | plan files under `docs/plans/*.md` (except README) missing from the Status Index | 0 (any positive is reportable) | none |
| Promotion | distinct citations of the same workflow theme (judgment-clustered; see skill step 4) since the promotion watermark | 3 | n/a |
| Fold-up (guidance repo only) | sibling-repo discipline-scope golden-rule candidates with independent lineage (not shared bootstrap ancestry) not yet reflected here — generalizations of agent-theory itself, never recurring product-engineering rules ([AT-THEORY-7] ascension boundary) | 2 independent incidents/adaptations | n/a |

Thresholds are declared here so the trigger check is mechanical, and they
are per-repo values: consumer repos calibrate their own (mm's volume needs
far higher triggers), and the derivation commands must be adapted to each
repo's ledger format. Tuning is legitimate; tune in this file with a
run-log note, not ad hoc.

**Report when (one sentence to the user):**

- harvest candidates ≥ the plans threshold, or
- unindexed > 0, or
- a reconsideration condition in the deferral table has fired and counts
  changed since `checked_through`.

Unchanged counts against an unchanged deferral row: do not re-nag.

## Reporting Cues (non-gating)

Derived counts worth reporting alongside the threshold check when cheap to
compute. They inform judgment and are never gates:

- **Apparatus share** — the fraction of active (non-retired) plan files
  whose subject is the process corpus itself (plans, docs, lessons,
  coalescing, skills). A sustained rise is evidence for the process-tower
  falsifier in `docs/program-theory.md` [AT-THEORY-6]; evaluate by
  judgment, not by budget.

## First-Sweep Policy (this repo — executed 2026-07-14, see run log)

Historical record of that sweep's constraints, demoted in place
2026-08-07: not current authority. Current sweeps are governed by the
[DOM-5]/[DOM-14] archive rule above — uncommitted sweeps may remove
retained-ref source-pinned material; only worktree-only sources force
additive-only.

- Lessons tier only. The plans tier is **not derivable** until the status
  index from plan §5.5 lands, and stays untouched in the first sweep
  regardless.
- Dedup is mandatory: many 2026-04-07 entries are already distilled into
  Golden Rules — those fold as pointers ("distilled as Golden Rule N"),
  never as duplicate rules.
- The four foundation plans are marked `exemplar` in the proposed status
  index and are exempt from retirement until superseded.
- (As executed 2026-07-14, under the then-current rule:) destructive
  steps required landing authorization, and the uncommitted first
  sweep stayed additive-only (drafts and candidates, no deletion, no
  watermark advance).

## Watermarks

| Tier | Distilled through | Source SHA |
|------|-------------------|------------|
| Lessons | 2026-04-07 | `5927481` |
| Plans | (none — no retirements yet; status index live) | — |
| Promotion | 2026-07-15 interface-review skill (citations: taut `4a129e9`, mm `b6bded5`, mm `15faadc`) | `30c8b04` (pre-promotion HEAD) |
| Fold-up | 2026-10-14 ecosystem fold-up wave (simplebroker `8a5578a`, taut `f4275a6`, weft `9b7ada69`, backstitch `7d627f3`, mm `16d96241f`) | `d52e12a` (pre-promotion HEAD) |

### Noncontiguous Lesson Fold Records

When a repository reclassifies older dated entries into a lesson section or
folds entries out of chronological order so a single date watermark cannot
bound remaining hot entries, that section ceases to use a date cursor and
tracks folds here instead (`[DOM-14]`):

| Fold ID | Section | Source SHA | Entries folded | Target surface |
|---------|---------|------------|----------------|----------------|
| (none yet in hub — single-list ledger remains monotonic) | — | — | — | — |

## Deferral State

A trip is only news when it is new: unchanged counts against this table do
not re-nag; a changed count or a fired reconsideration condition does.

| Tier | Checked through (date, SHA) | Counts at check | Reason deferred | Reconsider when |
|------|------------------------------|-----------------|-----------------|-----------------|
| Lessons | 2026-08-07, `2415252` | 22 past watermark — threshold 10 tripped, nothing foldable | All entries are within the 30-day age floor (2026-07-14 onward), are fold records/pointers (2026-07-02, 2026-04-07), or are cited by an active plan (2026-07-06, cited by the coalescing-layer plan) | Entries age past the floor (earliest batch: 2026-07-14 entries on 2026-08-13) or the coalescing-layer plan closes |
| Plans | 2026-08-07, `2415252` | 5 at check — threshold met; 3 soft-retired this sweep, 2 deferred → 2 remaining, under threshold | Deferred: 2026-07-15-coalescing-method-refinements (its §10 is the live disposition detail for the held fold-up candidates) and 2026-08-07-simplebroker-backport-wave (closed same day; its execution log is the cited live home of the OD-3 observation per the register plan's amendment) | Held fold-up candidates resolve or the register-conditioning delta lands; recount at next sweep |
| Unindexed | 2026-10-14, ecosystem fold-up wave, `d52e12a` | 1 found (`2026-08-07-commit-subject-principle-promotion-plan.md` from `a7cf45e`) → 0 after in-wave index repair in `docs/plans/README.md` | Not tripped after in-wave repair | Any positive count |
| Promotion | 2026-07-15, interface-review promoted | 3 citations of one theme (taut MCP plan §16.3–§16.4; mm impl/41 RiskEvaluationApi contract; mm external-API/MCP plan §4/§5/§9) — threshold 3 met | Promoted to `skills/interface-review/SKILL.md` per 2026-07-15-interface-review-skill-promotion-plan at source `2415252` (retired); not deferred | New distinct citations of another theme accumulate; recount at next sweep |
| Fold-up | 2026-10-14, ecosystem fold-up wave (`docs/plans/2026-10-14-ecosystem-fold-up-wave-plan.md`) | All 2026-07-15 (three-tier verification), 2026-07-17 (mm 4-item slate), and 2026-08-07 (SimpleBroker 8-item slate: 6 graduated, 2 closed per `[REV-AT-004]` Screen 2) candidates resolved + 2026-10-14 five-repo wave graduated; 1 held skill-only (framework-fact expiry for `[DOM-14]`) | **2026-10-14 ecosystem fold-up wave (simplebroker `8a5578a`, taut `f4275a6`, weft `9b7ada69`, backstitch `7d627f3`, mm `16d96241f`):** (1) **2026-07-15 three-tier verification** graduated to `[DOM-14]` (`mm` `dfd7aca23` + `taut` `6ae85c7` + `simplebroker` `5410aff` doc-only lightweight verification floor); **framework-fact expiry** remains held skill-only for `[DOM-14]` (still 1 true incident lineage in `mm` `127fd437d` / `mm` `712ea5440`, though refined in `skills/coalescing/SKILL.md` step 2.6 with in-situ version-qualification from `weft` `6f4bcd7d`). (2) **2026-07-17 `mm` 4-item slate resolved:** `reviewed-baseline` pin + `Revision Log` graduated to `docs/agent-context/runbooks/writing-plans.md` (`mm` `9d86d038e` + `weft` `fd544c33` + `simplebroker` `a38e6a9`); `findings-at-standing-boundaries-escalate` (`RECONSIDERATION REQUESTED`) graduated to `[DOM-11]`, `docs/agent-context/engineering-principles.md` §8, `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md` §4a/§5, and `skills/call-agent/SKILL.md` (`mm` `9d86d038e` + `taut` `cfd8799` + `weft` `ff91368e`); `standing-invariants-surface` reconciliation graduated to `docs/agent-context/runbooks/hardening-plans.md` §1 (`mm` `9d86d038e` + `simplebroker` `00b837f` `SM-*` manifest); `deployment-status qualifier axis` resolved by explicitly rejecting status-column deployment prose qualifiers in `docs/agent-context/runbooks/writing-plans.md` (`mm` `1bec386d5`, enforced by `taut` `3706d73` and `simplebroker` `4cb47bc` closed-vocabulary gates). (3) **2026-08-07 SimpleBroker 8-item slate resolved in full:** 2 items (`live-state check inside atomic boundary` and `cleanup authority from ownership + live state`) closed under `[REV-AT-004]` Screen 2 as product-engineering preconditions owned by product theories (while `docs/agent-context/runbooks/hardening-plans.md` §13 and §15 record only the discipline-level planning duties to identify the owning product cleanup contract and stale-remote publication guard); 6 items graduated (`simplebroker` `a38e6a9` + multi-repo lineages across `docs/agent-context/engineering-principles.md` §2/§4/§10/§11/§12, `docs/agent-context/decision-hierarchy.md`, `docs/agent-context/principles.md`, `docs/agent-context/runbooks/writing-plans.md`, `docs/agent-context/runbooks/writing-specs.md`, and `docs/agent-context/runbooks/testing-patterns.md`). (4) **New 2026-10-14 cross-repo discipline promotions:** Tier-1 cross-family vs Tier-2 native-subagent review hierarchy (`simplebroker` `f18b9c6`, `weft` `fd544c33`); deliberate friction replaces lost social friction in `[AT-THEORY-4]` (`simplebroker` `f18b9c6`); contention reduction as a theory-possession stop-condition (`simplebroker` `5410aff`, `weft` `9b7ada69`); returning mid-task on falsified premises (`weft` `ff91368e`, `simplebroker` `8a5578a`); exact CI-root verification (`taut` `f4275a6`, `simplebroker` `8a5578a`); delegated RED transcript verification (`weft` `fd544c33`, `mm` `16d96241f`); P1 mutation line (`taut` `3d038f5`, `mm` `16d96241f`, `simplebroker` `8a5578a`); static complexity as visibility signal + governed suppression registries (`simplebroker` `49da9b2`, `simplebroker` `00b837f`, `taut` `eabc272`); all-eligible plan-tier sweep rule + noncontiguous lesson fold records + `- YYYY-MM-DD: (revised ...)` ordering (`taut` `58469b3`, `taut` `a86d669`, `mm` `7bc8b6bf7`); and gate upgrades to `bin/check-doc-paths`, `bin/check-dom15-fixtures`, and `bin/coalesce-check` (`simplebroker` `4cb47bc`, `taut` `3d038f5`, `weft` `7c245c91`, `backstitch` `bd4a8cd`) | Second repo exercises an actual framework-fact expiry fold or durably installs the expiry disposition path; next sibling sweep |

## Run Log

One line per run, newest first. Each line is a claim; it must survive a
spot-check against the diff. `checked-deferred` lines are valid runs. Source
SHA names a commit verifiably containing the raw material; the fold commit
may be appended as metadata once it exists.

| Date | Tier(s) | Source SHA | Claim |
|------|---------|------------|-------|
| 2026-10-14 | Fold-up + Unindexed (five-repo ecosystem wave) | simplebroker `8a5578a`, taut `f4275a6`, weft `9b7ada69`, backstitch `7d627f3`, mm `16d96241f` (foreign); pre-promotion HEAD `d52e12a` | Ecosystem fold-up wave per `docs/plans/2026-10-14-ecosystem-fold-up-wave-plan.md` (Class 5+P): graduated the 2026-07-15 three-tier fold verification to `[DOM-14]`, resolved the 2026-07-17 `mm` 4-item slate and the 2026-08-07 SimpleBroker 8-item slate (6 graduated, 2 closed as product-engineering rules under `[REV-AT-004]` Screen 2), promoted cross-repo discipline rules across `[DOM-10]`/`[DOM-11]`/`[DOM-14]`, `docs/program-theory.md` `[AT-THEORY-4]`, `AGENTS.md`, `docs/agent-context/principles.md`, `docs/agent-context/decision-hierarchy.md`, `docs/agent-context/engineering-principles.md` (§2, §4, §8, §10, §11, §12, §14), six runbooks, three skills, and three executable gates (`bin/check-doc-paths`, `bin/check-dom15-fixtures`, `bin/coalesce-check`), and repaired 1 unindexed plan row (`2026-08-07-commit-subject-principle-promotion-plan.md` from `a7cf45e`) in `docs/plans/README.md`. Fold-up watermark advanced to 2026-10-14; full inventory in `CHANGELOG.md` 2026-10-14. |
| 2026-08-07 | Plans (deletion follow-up, correction) | `2415252` | The optional codex verification (dispatched pre-rule-change, reporting post-deletion) confirmed two plans clean and found three record defects on guidance-gates: ledger absorption misattributed (CHANGELOG 2026-08-06 does not record that wave; bin/bootstrap-agent-theory omitted) and the origin/main-hardcoding limitation from its review F4–F5 preserved nowhere. All repaired in place: ledger row corrected with revision marker, limitation extracted to docs/lessons.md plus a code comment at the check site. The deletion stands — content retrievable at `2415252`; the defects were in surviving records, which is exactly what in-place repair under git-backed reversibility is for. |
| 2026-08-07 | Plans (deletion follow-up) | `2415252` | Physical deletion of the three retired-pending plans (specs-index-renumbering, interface-review-promotion, guidance-gates) under the amended retirement rule: recorded harvest gates re-checked from the current tree, retrieval from `2415252` verified pre- and post-deletion, ref-reachable via origin/main, no live-path backlinks outside docs/plans/. Second-agent verification optional per owner decision (a codex verification dispatched under the prior rule is noted as corroboration when it reports). Index rows removed; ledger lines are the surviving record. Class 2 archive maintenance. |
| 2026-08-07 | Lessons + Plans (authorized sweep) | `2415252` | Sweep authorized by owner after the backport-wave landing, run under the new [DOM-5]/[DOM-14] archive rule (routine, Class 2 — no durable guidance promoted). Lessons: threshold tripped (22 past watermark), nothing foldable — all hot, fold records, or active-cited; checked-deferred with conditions. Plans: 5 candidates at threshold; harvest gates run; soft-retired 3 (specs-index-renumbering, guidance-gates, interface-review-promotion — index flipped to retired-pending, backlinks converted to source-pinned form at `2415252`, ledger lines written); deferred 2 with recorded reasons (method-refinements §10 live disposition detail; backport-wave is the cited OD-3 observation home). One lesson added (pipeline-exit masking, from pre-landing F1). No physical deletion (dedicated follow-up after second-agent gate verification); no watermark advanced (nothing folded). Traceability gates rerun post-sweep, exit codes captured directly: check-doc-paths 0, coalesce-check 0 (`2415252` reported local-only pending push — publication is the owner's call), check-dom15-fixtures 0. |
| 2026-08-07 | Fold-up (backport wave, not a sweep) | SimpleBroker pin `a38e6a9` (foreign); landed here at `2415252` | Backport wave per `docs/plans/2026-08-07-simplebroker-backport-wave-plan.md` (Class 5+P, three-round review): [DOM-5]/[DOM-14]/[DOM-15] archive-rule promotion (OD-1); demotion-in-place graduated by owner direction (OD-2); existence-check rule promoted by owner direction (OD-4); eight-candidate SB slate registered at 1 lineage in the Fold-up deferral row; Unindexed tier added; `coalesce-check` shallow-skip contract change. Nothing folded; no watermark advanced; full inventory in `CHANGELOG.md` 2026-08-07. |
| 2026-07-28 | — (gate correction; nothing folded) | — | **`coalesce-check` no longer probes the filesystem for sibling repositories.** `SIBLING_ROOT = REPO_ROOT.parent` hardcoded a checkout layout no document declared — invisible from inside the repo, absent in a fresh clone or CI — and, worse, it reported SHAs resolvable only in a neighbouring working copy as *verified*, laundering a local-only claim into a green check and defeating the cue-portability rule the tool exists to enforce. Now: a repo verifies its own SHAs locally and against its own published remote; SHAs it cannot resolve are reported as **foreign claims** with the repository they name (informational, never a verdict); an unresolvable SHA that names *no* repository is a genuine failure, because a cue must say where it is retrievable. Optional `COALESCE_SIBLING_ROOT` gives local convenience, off by default, reported separately and never as verification. Landed across all seven repositories; mm's first corrected run found a real unattributed hub cue, repaired in the same wave. |
| 2026-07-28 | — (repository rename; nothing folded) | — | **Renamed `agent-guidance` → `agent-theory`** (owner decision): the repository names an intellectual discipline — theory-building for agent-assisted development, in Naur's sense — not an artifact of instructions supplied to agents. Working-tree references were rewritten in full across all seven repositories, including historical provenance lines and plan filenames; the repository is private, so the immutability rule's protection (external readers holding claims made under the old name) does not yet apply. **Git commit messages and published history retain `agent-guidance`** — rewriting those would require rebasing seven repositories and would invalidate every `source_sha` cue the coalescing layer depends on. The GitHub remote and the conceptual reframing of the corpus's own self-description (`agent-context`, "guidance wave", the artifact-frame vocabulary) are tracked separately as owner work. |
| 2026-07-28 | Fold-up | taut `3706d73` (source; contains the checker, tests, and skill text) | Two taut inventions folded up by owner direction: repair-in-sweep doctrine → hub coalescing skill step 1 (1 durable lineage; hub/weft ad-hoc practice not counted — shared ancestry with the triggering review); structured status-index contract (`status-review` quarantine, executable index gate, never-fall-back) → writing-plans Plan Lifecycle + the skill's derivation chain (2 lineages: taut mechanism + mm's independently-invented free-text quarantine). Vocabulary reconciliation owed at consumers' next touch: free-text ambiguity phrases migrate to `status-review`. Tool itself (check-plan-status-index) stays taut-local until a hub/consumer port is separately justified. Role-symmetry note: taut had not yet proposed upward; the hub's observation of `3706d73` is the fold-up trigger. |
| 2026-07-28 | — (correction record; nothing folded) | — | The 2026-07-14 coalescing-layer pilot gate closed with criteria 3–4 (retrieval friction; measured context savings) unevaluated — its satisfaction note covered false positives, format misses, and run-log spot-checkability only, and propagation proceeded. The closed plan is immutable, so this line is the correction: **measurement debt is open**. Two of four criteria for the layer's cost side have never been instrumented; the owner holds the decision on adopting the per-task log (class, plan-existed, review-caught, reopened) proposed by the 2026-07-28 external review. Until measured, claims that the layer pays for its context cost rest on qualitative evidence only (weft's tripped-threshold honesty; this week's review catch-rate). |
| 2026-07-15 | Promotion | `30c8b04` (pre-promotion HEAD); citations taut `4a129e9` (§16.3 committed; §16.4 working-tree in its authoring session), mm `b6bded5` (RiskEvaluationApi contract), mm `15faadc` (external-API/MCP plan) | [DOM-14] promotion tier tripped at 3 distinct citations of the agent-facing-interface-review theme. Promoted `skills/interface-review/SKILL.md` (procedure wrapping `designing-agent-facing-interfaces.md`: checklist walk, enumerable-gates step, MCP annotation/description verification, file:line evidence bar; findings-table + ratified-judgments + verdict + runbook-feedback output contract). Opus-drafted, grok-reviewed (PASS-with-changes; 8 findings applied, incl. the skill's own teaching example failing its file:line bar — see plan §4). Registered in repository-map §Skills; runbook back-pointer added. No lessons/plans material folded; those watermarks unmoved. |
| 2026-07-15 | Fold-up + promotion | `5b990ad` (pre-promotion HEAD); evidence mm `3487ec358`/`127fd437d`/`5e8fb8ca7`/`c6356186a`/`63f87cadb`/`a9d17383e`, weft `8382a4d5` | Coalescing-method-refinements amendment (Class 5+P, grok-reviewed): six refinements integrated into `skills/coalescing/SKILL.md`; [DOM-14] trigger bullet promoted (fold-unit denomination + declared progress model, F7 tighten); verification and decay bullets **held skill-only** per review F2/F3 (single lineage — weft's expiry check was a true-negative, not a second incident/adaptation). Two drafting-pass evidence errors corrected at review (F1 weft-check-did-run; F4/F5 SHA mis-pins). Weft's run-log recording gap patched in weft same-day. No raw material folded; no lessons/plans watermark moved. |
| 2026-07-14 | Fold-up | mm `9a8d17d55` (contains mm's proposal record and the harvested source) | First role-symmetric fold-up accepted: mm's agent-API design principles (proposed by mm's root-docs retirement sweep) distilled into `runbooks/designing-agent-facing-interfaces.md`, scaffolded via COPIED_FILES. Lineage accounting per `docs/plans/2026-07-14-agent-facing-interfaces-runbook-plan.md` §2: dual-lineage convergence for two principles (meets the 2-independent threshold), single-lineage generalization by explicit owner direction for the rest, one convergence claim withdrawn as shared-ancestry. Raw material: mm's retired `system_api_design.md` (full text at mm `2b0182200`) and its `implementation/53`. |
| 2026-07-14 | Lessons | `5927481` | First sweep (authorized): folded 12 bootstrap-era entries (2026-04-07) into one pointer line — pure dedup, every entry verified already distilled into [DOM-*] sections, Golden Rules 7–8, or runbooks; no new rules, no Golden Rule changes. Kept 2026-07-02 and 2026-07-06 verbatim (age floor; cited by active plan). Watermark advanced to 2026-04-07. Plans/promotion/fold-up untouched per First-Sweep Policy. Backstitch: clean. |
| 2026-07-14 | — (promotion, not a sweep) | `5927481` | [DOM-14] and deltas §5.1–§5.7 promoted per plan task 3: DOM spec gains §14; engineering-principles gains §15; writing-plans gains Plan Lifecycle and Retirement; maintaining-traceability gains the retired-citation form; plans README gains Status Index + Retired Plans; agent-context README and context.index.yaml gain the hot-lessons projection; lessons.md intro notes startup scope. Nothing folded; no watermark advanced. |
| 2026-07-14 | all | — (additive-only; nothing folded) | Checked-deferred with blockers; see Deferral State. Review passes 1–2 dispositions applied: read-only trigger check, source_sha cue model, additive-only-when-uncommitted, plan mutability boundary, deferral state model, multi-signal decay, independent-lineage fold-up. No fold performed; no watermark advanced. |
| 2026-07-14 | — | — | Layer initialized by docs/plans/2026-07-14-coalescing-layer-plan.md. Derived counts at initialization: lessons 14 entries past (no) watermark; plans 5 completed-unretired by file inspection. |
