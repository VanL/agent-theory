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
| Fold-up (guidance repo only) | sibling-repo golden-rule candidates with independent lineage (not shared bootstrap ancestry) not yet reflected here | 2 independent incidents/adaptations | n/a |

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
| Fold-up | 2026-07-15 fold-unit trigger denomination (mm `3487ec358`, weft `8382a4d5`) | `5b990ad` (pre-promotion HEAD) |

## Deferral State

A trip is only news when it is new: unchanged counts against this table do
not re-nag; a changed count or a fired reconsideration condition does.

| Tier | Checked through (date, SHA) | Counts at check | Reason deferred | Reconsider when |
|------|------------------------------|-----------------|-----------------|-----------------|
| Lessons | 2026-07-14, first sweep executed | 2 past watermark — under threshold 10 | Not tripped | Count changes |
| Plans | 2026-07-14, `5927481` | 1 (specs-index-renumbering; four others are exemplar) — under threshold 5 | Not tripped | Count changes |
| Unindexed | 2026-08-07, backport wave, `2415252` | 0 | Not tripped | Any positive count |
| Promotion | 2026-07-15, interface-review promoted | 3 citations of one theme (taut MCP plan §16.3–§16.4; mm impl/41 RiskEvaluationApi contract; mm external-API/MCP plan §4/§5/§9) — threshold 3 met | Promoted to `skills/interface-review/SKILL.md` per `docs/plans/2026-07-15-interface-review-skill-promotion-plan.md`; not deferred | New distinct citations of another theme accumulate; recount at next sweep |
| Fold-up | 2026-07-15, coalescing-method-refinements amendment landed (grok-reviewed) | 2 accepted (agent-interface principles, 2026-07-14; fold-unit trigger denomination, 2026-07-15); 1 held skill-only (framework-fact expiry) — see `docs/plans/2026-07-15-coalescing-method-refinements-plan.md` §10 | Trigger denomination (mm recalibration `3487ec358` + weft date-cursor failure `8382a4d5`): two independent lineages — graduated into the [DOM-14] trigger bullet and the skill's step 1. Framework-fact expiry: mm is the single incident lineage (fold `127fd437d`, disposition `712ea5440`); weft's check **did run** at a real pin bump (`8382a4d5` commit message; pin bump `57255b83`) but was a true-negative — zero expiries, no disposition path exercised — and review disposed (F2) that a true-negative validates the check, not the phenomenon: **held skill-only** with the three-tier verification bullet (F3), both awaiting a second lineage. Four further refinements landed skill-only by design (examples-are-claims, catch-all check, collision-aware landing, plus the held pair). **Candidate slate registered 2026-07-17 from mm's lifecycle-rollback process hardening** (mm plan `2026-07-17-process-hardening-after-lifecycle-rollback.md`), all at 1 lineage: revision re-gate + reviewed-baseline pin + Revision Log (mm incident; hub Plan Lifecycle carries a pointer-grade caution citing it); findings-at-standing-boundaries-escalate (1 clean lineage — the interface-review disposition practice is noted but flagged shared-ancestry, does not count as second); standing-invariants-registry pattern; deployment-status qualifier axis (ratified locally in mm's plans README). The commit-scope rule was judged at 2 independent lineages (weft benign omnibus, mm harmful omnibus) and landed as a hub lesson. **2026-08-07 backport wave (SimpleBroker pin `a38e6a9`):** demotion-in-place of superseded plan text **graduated by owner direction** into `writing-plans.md` Plan Lifecycle (lineages: mm incident + SB pre-release plan "Superseded Owner Amendment" section — SB partial, its runbook carries the hub's mm caution); Revision Log + reviewed-baseline pin stay candidates with SB recorded as partial family evidence (SB plan has a `Revision:` header and outranking owner amendments but no Revision Log table and no baseline pin); revision re-gate already normative, leaves the slate. **SB candidate slate registered, all 1 SB lineage, graduate on second lineage or owner direction** (sources in SB `docs/lessons.md` at the pin): live-state check inside atomic boundary for global-invariant mutations (:244-250); "unused" searches include examples + ungated consumers (:194-197); handshake peers declare protocol literals independently (:209-213); cleanup authority from ownership + live state, not path names (:234-237); resolved config flows through every validation boundary (:238-243); counted/completeness claims verified mechanically, "full" made true not weakened (:166-173); extraction audits removed paragraphs for hazards (:160-165); lock-order corrections not substituted by retry, mocks hide the cycle (:204-208) | An actual second-repo expiry fold, or a second repo durably installs the expiry disposition path; second independent lineage or explicit owner direction for the 2026-07-17 slate; recount at the next sibling sweep |

## Run Log

One line per run, newest first. Each line is a claim; it must survive a
spot-check against the diff. `checked-deferred` lines are valid runs. Source
SHA names a commit verifiably containing the raw material; the fold commit
may be appended as metadata once it exists.

| Date | Tier(s) | Source SHA | Claim |
|------|---------|------------|-------|
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
