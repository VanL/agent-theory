# Coalescing Layer Plan

Status: Active — two independent review passes dispositioned (§8a);
promotion slice (task 3) applied 2026-07-14; guidance wave committed as
`5927481` (task 4). Remaining: first sweep (task 5), pilot gate (task 6).
Promotion baseline identifier: `5927481`.
Plan type: spec-authoring / guidance revision (with two new additive files)
Risk level: process-changing, boundary-crossing (alters plan lifecycle and
lessons retention across every adopting repo)

## 1. Goal

Establish the compounding layer as an explicit, event-triggered process:
a periodic coalescing sweep that distills the lessons ledger, harvests and
retires completed plans, and promotes recurring workflows to skills — adopting
Engram's tiered-memory principles on a files-plus-git substrate, without
depending on Engram. Files in the working tree are the source of truth for
current state; git history is the only archive.

## 2. Source Documents

Source specs:
- `docs/specs/01-development-documentation-operating-model.md`
  [DOM-2], [DOM-5], [DOM-8], [DOM-9], [DOM-12]

Source runbooks and context:
- `docs/agent-context/runbooks/skills-lifecycle.md` (promotion rule)
- `docs/agent-context/runbooks/writing-plans.md` (plan shape; §4b–4d)
- `docs/agent-context/runbooks/maintaining-traceability.md` (backlink rules)
- `docs/agent-context/engineering-principles.md` (meta-principle: compound
  knowledge; §12 gates; §13 declared variation)

External design source (thesis only, no dependency taken):
- the Engram repository's memory model and context-assembly specs
  (`../engram/docs/specs/10-minimum-memory-model.md`,
  `../engram/docs/specs/13-context-assembly-and-arcs.md`). Principles
  adopted: additive coalescing with mandatory retrieval cues back to
  constituents; semantic-boundary (not fixed-count, not calendar) triggers;
  verbatim-recent tier; multiplicative importance with a floor for durable
  rules; contradiction resolved by explicit in-place edit (file-native
  improvement over decay).

## 3. Context and Key Files

Current structure the implementer must know:

- `docs/lessons.md` is an append-only dated ledger with a hand-distilled
  "Golden Rules" section. It grows without bound (mm's equivalent is ~2,800
  lines). The Golden Rules section is an arc-tier summary already being
  maintained manually.
- `docs/plans/` holds dated plans. `docs/plans/README.md` states rules but has
  no status index and no retirement mechanism. Sibling repos treat completed
  plans as immutable historical records (taut excludes them from doc-reference
  scanning; weft indexes them by status).
- `.backstitch.toml` configures backstitch over this docs-only corpus with
  `plan_roots = ["docs/plans"]`. Path claims in scanned docs must resolve;
  retired-plan references must therefore use a non-path citation form.
- `skills/` contains only `README.md` and `_template/SKILL.md`. The template
  section order is the required skill shape.
- The worktree currently carries a large uncommitted guidance wave (the
  2026-07-02 verification-lessons fold and 2026-07-06 cohesion principle).
  Downstream repos recorded "record the commit SHA when agent-guidance
  commits" provenance debt against it.

Files created by this plan (additive, land with the plan):
- `skills/coalescing/SKILL.md` — the coalescing sweep skill
- `docs/coalescing.md` — per-repo coalescing state: declared thresholds,
  watermarks, and the run log

Files edited only after review, per the deltas in §6:
- `docs/specs/01-development-documentation-operating-model.md` (new [DOM-14])
- `docs/agent-context/engineering-principles.md` (new §15)
- `docs/agent-context/runbooks/writing-plans.md` (plan lifecycle + retirement)
- `docs/agent-context/runbooks/maintaining-traceability.md` (retired-plan
  citation form)
- `docs/plans/README.md` (status index + retired-plans ledger)
- `docs/agent-context/README.md` (maintenance-rule pointer to the sweep)

## 4. Invariants and Constraints

- **Additivity before destruction — across commit boundaries.** Every
  coalescing run is two-phase: distill first (summary written, links
  verified), retire second (raw material removed). Never one motion. A
  failed distillation must leave the raw material untouched. The destructive
  phase (deleting raw entries, advancing watermarks, retiring plans)
  additionally requires commit authorization: in an uncommitted-review
  session, coalescing is additive-only — draft distillations and retirement
  candidates, propose provenance, delete nothing, advance nothing.
- **The session-start trigger check is read-only.** A tripped threshold is
  reported to the user, never acted on. All coalescing writes — including
  checked-deferred records — happen only inside an authorized maintenance
  task. Repository guidance cannot broaden the authority granted by the
  current request.
- **Every fold leaves a retrieval cue.** Distilled summaries and ledger lines
  carry the date range and a `source_sha` — a pre-fold commit that contains
  the raw material, known and verifiable (`git show <sha>:<path>`) before any
  editing begins. The fold commit itself cannot serve as the cue: a commit
  cannot contain its own hash, and the commit that deletes the raw entries
  does not contain them. The fold commit may additionally be recorded in the
  run log after it exists. A summary that cannot lead back to its
  constituents is broken even if it reads well.
- **The immediate tier stays verbatim.** The sweep must not fold lesson
  entries younger than the declared age floor, cited by an active plan, or
  part of a still-open theme.
- **Golden rules and safety invariants never decay.** Importance floor: lack
  of recent citation is never grounds to drop a golden rule or a safety rule.
- **Plan mutability has a boundary, and closure seals it.** While a plan is
  active, its task instructions and checklists stay current and mutable
  (per `maintaining-traceability.md` — stale instructions are worse than
  edited ones); its decision, deviation, and review logs are append-only.
  At closure the whole plan becomes immutable. Deletion only after the
  harvest gate (deviation log closed; durable rationale absorbed; lessons
  extracted; backlinks converted) — not waivable. A superseded plan
  requires the successor to name what it inherits before the predecessor
  retires.
- **Counters are derived, never stored.** Trigger counts are computed from
  the watermark and the current tree/history. The only stored coalescing
  state is the watermark and the run log in `docs/coalescing.md`.
- **Thresholds trigger attention, not action.** A tripped threshold means
  "run the sweep," not "fold exactly N items." A sweep that finds nothing
  foldable records a checked-deferred line; that is valid deferral, not a
  skipped obligation.
- **Run-log entries are claims and must survive a diff spot-check.** Each
  fold line enumerates what was folded into what.
- **No second archive.** No `docs/plans/retired/` or similar directory. Git
  is the only time machine; the in-tree projection of retired material is
  one ledger line per item.
- **Backstitch compatibility.** Retired-plan citations use a non-path form so
  the self-corpus check stays clean; verify with a backstitch run before and
  after the first retirement.

## 4a. Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## 4b. Spec Baseline

- Commit `9beb807` plus the current uncommitted worktree state (the
  2026-07-02/2026-07-06 guidance wave). The DOM spec file itself is clean at
  `9beb807`. This plan should land after or with a commit of the pending
  wave so downstream repos can pin one SHA for both.

## 5. Proposed Guidance Delta

Promotion strategy: D — spec-authoring / guidance revision. No code cites
these sections; apply the deltas directly after independent review, in one
slice, together with the two new additive files.

### 5.1 `docs/specs/01-development-documentation-operating-model.md` — insert new section after [DOM-13]

> ## 14. Coalescing and Memory Maintenance [DOM-14]
>
> The documentation surface is a tiered memory. Raw, dated records (lesson
> entries; completed plans) are the moment tier. Distilled rules (golden
> rules, runbook amendments), the plans ledger, and promoted skills are
> summary tiers. The working tree holds only the current, assembled state;
> git history is the archive. Docs change in place to match reality — going
> back in time is git's job, not the working tree's.
>
> Requirements:
>
> - each repository keeps coalescing state in `docs/coalescing.md`: declared
>   per-tier thresholds, per-tier watermarks, and a one-line-per-run log
> - coalescing triggers are event-derived, not calendar-based: counts are
>   computed from the watermark and the current tree, never stored
> - the session-start trigger check is read-only: a tripped threshold is
>   reported to the user, never acted on mid-task. All coalescing writes —
>   including checked-deferred records — happen only inside an authorized
>   maintenance task (user request, or agreed completion-boundary work).
>   Silently ignoring a trip is the only invalid response; reporting costs
>   one sentence
> - coalescing is additive-first across commit boundaries: distillation
>   drafts and retirement candidates may exist uncommitted; deleting raw
>   material, advancing watermarks, and retiring plans require a
>   landing-authorized phase with a durable checkpoint
> - deferrals have real state: a checked-deferred record carries
>   `checked_through` (date and SHA), the derived counts, the reason, and a
>   reconsideration condition — so an unchanged count does not re-nag every
>   session, and a changed count does
> - coalescing is two-phase and additive-first: distill, verify links and
>   cues, then retire; every fold leaves a retrieval cue — the date range
>   plus a `source_sha`, a pre-fold commit that verifiably contains the raw
>   material — in the surviving summary or ledger line. The fold commit may
>   be recorded in the run log after it exists, but it is never the cue
> - recent or still-cited raw material stays verbatim; golden rules and
>   safety invariants carry an importance floor — exempt from automated
>   decay, changed only by explicit revision, supersession, or deprecation
>   with a `(revised YYYY-MM-DD; was: <gist>)` marker
> - active plans keep instructions mutable and logs append-only, and become
>   immutable at closure; retirement is two-step — the sweep soft-retires
>   (status `retired-pending`, backlinks converted, ledger line written)
>   only after the harvest gate in `runbooks/writing-plans.md` passes, and
>   physical deletion happens in a dedicated follow-up change after the
>   gate is independently verified; plans marked `exemplar` in the status
>   index are exempt until their exemplar role is superseded
> - run-log entries are claims: each fold line must be spot-checkable
>   against the diff of the fold commit
>
> Owner: whoever the sweep check nags — any agent that observes a tripped
> threshold at session start. Boundary: applies to lessons, plans, runbook
> and skill promotion, and (for the guidance repo) cross-repo fold-up; specs
> and implementation docs are living documents maintained per [DOM-6] and
> [DOM-7], not coalesced. Verification: the run log plus the repository's
> traceability gate. Required action: when a threshold is tripped, report
> the trip state; respond with a sweep or a checked-deferred line per the
> trigger rules above.

### 5.2 `docs/agent-context/engineering-principles.md` — insert new §15 before "Warning Signs"

> ## 15. Coalesce on Events, Not Time; Every Fold Keeps a Cue
>
> Ledgers and plan directories are moment streams: raw, dated, append-only
> in spirit. Left alone they grow until agents stop reading them. The fix is
> periodic coalescing — distill cold entries into rules, harvest and retire
> completed plans, promote recurring workflows to skills — governed by three
> rules borrowed from tiered-memory design:
>
> - **Trigger on accumulation, not on the calendar.** Repos have different
>   pulse rates; event counts derived from a watermark scale automatically.
>   A stored counter is state that drifts; a derived count is always honest.
> - **Keep the recent tier verbatim.** Never summarize young, hot, or
>   still-cited entries — that destroys exactly the detail the next session
>   needs. Fold only what is cold and stable.
> - **A summary that cannot lead back to its constituents is broken, even if
>   it reads well.** Every fold leaves a date range and commit SHA in the
>   surviving line. Git is the archive; the cue is what makes the archive
>   reachable.
>
> Promotion and decay are citation-driven, not vibes-driven: an entry cited
> by later plans and reviews is promotion evidence; an uncited entry whose
> subject has churned is decay evidence. Presence in the always-read context
> is not evidence of usefulness — only explicit citation in work products
> counts. Golden rules and safety invariants carry an importance floor and
> never decay. Contradiction is resolved by editing the rule in place — with
> a revision marker `(revised YYYY-MM-DD; was: <gist>)` when the meaning
> changes, so citations to the rule stay interpretable across history — and
> the old version lives in git.

### 5.3 `docs/agent-context/runbooks/writing-plans.md` — insert new section after "Backlink Rule"

> ## Plan Lifecycle and Retirement
>
> Plans move through: `draft` → `active` → `completed` or `superseded` →
> `retired`. Status lives in the plan index (`docs/plans/README.md`), not in
> ceremony inside the plan file.
>
> - **Active plans have a mutability boundary**: task instructions and
>   checklists stay current and mutable — stale instructions are worse than
>   edited ones, and git preserves prior versions; decision, deviation, and
>   review logs are append-only. At closure the whole plan becomes
>   immutable.
> - **Completed and superseded plans are harvest candidates.** They stay in
>   the tree until the coalescing sweep retires them.
> - **The harvest gate — all four before deletion, no exceptions:**
>   1. deviation log closed (no `pending` spec proposals)
>   2. durable rationale absorbed into the governing spec or implementation
>      doc (or explicitly judged not durable)
>   3. lessons extracted to `docs/lessons.md` where applicable
>   4. every spec `## Related Plans` backlink converted to the retired
>      citation form (see `maintaining-traceability.md`)
> - **Superseded plans additionally require** the superseding plan to name
>   what it inherits (open deviation rows, decided-but-unbuilt behavior)
>   before the predecessor retires.
> - **Retirement is two-step: soft-retire, then delete.** The sweep performs
>   the soft retirement — status flips to `retired-pending` in the index,
>   backlinks convert to the retired citation form, and the ledger line is
>   written (name, date range, one-sentence outcome, what absorbed it,
>   source SHA). Physical deletion happens in a dedicated follow-up change only
>   after a second agent or the user verifies the harvest gate. Never
>   soft-retire and delete in the same change, and never create a
>   retired/archived plans directory — git is the archive.
> - **Exemplar plans are exempt.** The status index may mark a plan
>   `exemplar` (bootstrap or operating-model foundation plans that serve as
>   onboarding examples). Exemplars are not retirement candidates until the
>   index note says their exemplar role has been superseded.
> - Record the source SHA as a mainline commit that actually contains the
>   plan's final state; with squash merges, the squashed mainline commit is
>   the one to cite.

### 5.4 `docs/agent-context/runbooks/maintaining-traceability.md` — insert under "Completion Gate", after the existing bullets

> Retired-plan citation form: when a plan is retired, spec backlinks change
> from a live path to a non-path citation:
> `- retired: 2026-05-02-example-plan — source <source_sha>; see the ledger
> in docs/plans/README.md`. The source SHA is a commit verifiably
> containing the plan file. This keeps the traceability gate clean (no dead
> path claims) while preserving the retrieval cue. Do not leave live-path
> backlinks to deleted plans, and do not delete the backlink itself — the
> spec's plan history remains part of its record.

### 5.5 `docs/plans/README.md` — append new sections

> ## Status Index
>
> | Plan | Status |
> |------|--------|
> | 2026-04-07-bootstrap-scaffold-plan.md | completed — exemplar (bootstrap onboarding example) |
> | 2026-04-07-development-documentation-foundation-plan.md | completed — exemplar (operating-model foundation) |
> | 2026-04-07-plan-hardening-guidance-plan.md | completed — exemplar (hardening example) |
> | 2026-04-07-review-skills-bootstrap-plan.md | completed — exemplar (review-loop example) |
> | 2026-04-07-specs-index-renumbering-plan.md | completed |
> | 2026-07-14-coalescing-layer-plan.md | draft |
>
> ## Retired Plans
>
> One line per retired plan; the body lives in git at the fold SHA.
>
> | Plan | Dates | Outcome | Absorbed into | Source SHA |
> |------|-------|---------|---------------|------------|

### 5.6 `docs/agent-context/README.md` — add to "Maintenance Rules"

> - When `docs/coalescing.md` shows a tripped threshold, report it and
>   respond per [DOM-14]: a checked-deferred line with derived counts, or a
>   full sweep (its own unit of work) on user request, at twice the
>   threshold, or at a completion boundary.

### 5.7 Context projection — `docs/agent-context/README.md` read order and `docs/lessons.md` header

Amend the read-order entry for lessons (and the corresponding line in
`context.index.yaml`'s read order) to:

> `docs/lessons.md` — required startup reading is the **Golden Rules
> section plus dated entries after the lessons watermark** (see
> `docs/coalescing.md`). Older entries are searchable reference material,
> not startup context.

And add one line to the `docs/lessons.md` intro:

> Startup context is the Golden Rules plus entries after the watermark in
> `docs/coalescing.md`; the rest of this ledger is searchable history.

This fixes context selection independently of any storage coalescing: the
hot tier shrinks the moment the watermark advances, whether or not old
entries are ever physically folded.

## 6. Tasks

1. Land the two additive files with this plan (this slice):
   - `skills/coalescing/SKILL.md`
   - `docs/coalescing.md`
   - Done signal: files exist, follow `skills/_template/SKILL.md` section
     order, and cite [DOM-14] as proposed.
2. Independent review of this plan and the §5 deltas (see §8). Blocker for
   task 3.
3. Guidance-promotion slice: apply §5.1–§5.7 exactly, in one change, after
   review dispositions are recorded. §5.7 (context projection) is the
   highest-value piece and must not be dropped if the slice is trimmed:
   most of the read-tax pain is context selection, not stored history.
   - Done signal: deltas applied verbatim or with review-driven edits noted
     in the deviation log; `## Related Plans` in the DOM spec gains this
     plan.
3b. Scaffold integration (added post-promotion, per review pass 1 item #7's
   inventory-drift concern): `skills/coalescing/SKILL.md` added to
   COPIED_FILES; `docs/coalescing.md` added as a GENERATED_FILE with a
   fresh-state template (per-repo state must never be copied verbatim);
   repository-map and documentation-system renderers and the generated
   lessons intro updated to match; skill status line genericized for
   consumers. Verified by scaffolding into a scratch directory: both
   artifacts created, generator renders correctly.
4. Commit the pending guidance wave together with (or before) this work so
   downstream repos can pin one SHA. Do not commit without the user's
   go-ahead; if review happens uncommitted, report the state explicitly.
5. First sweep in this repo — conservative scope, after task 3 only:
   - lessons tier only; the plans tier is not derivable until the §5.5
     status index lands and stays untouched this sweep regardless
   - before drafting any distillation, check each candidate cluster against
     the existing Golden Rules and engineering-principles sections — many
     2026-04-07 entries are already distilled; for those the fold is a
     pointer ("distilled as Golden Rule N"), never a duplicate rule
   - Done signal: `docs/coalescing.md` run log has a fold or
     checked-deferred entry whose claims survive a diff spot-check.
6. Pilot gate: run at least **two** real sweeps in this repo and evaluate
   false positives, missed formats, retrieval friction, and measured
   context savings before any propagation.
7. Follow-up (separate work, out of this plan's scope, blocked on task 6):
   propagate to mm, taut, weft, backstitch, engram with SHA-pinned
   provenance — including per-repo threshold calibration (mm's ledger and
   plan volume need much higher trigger values than this repo's defaults)
   and adaptation to each repo's ledger format (the dated-bullet grep is
   this repo's shape, not a portable contract); optionally add an
   executable `coalesce-check` script once any repo wants the gate in CI.

## 7. Testing Plan / Verification and Gates

Docs-only change; verification is by inspection plus the corpus gates:

- backstitch self-corpus run with the committed `.backstitch.toml` before
  and after the guidance-promotion slice — no new errors or warnings
- grep gates: every §5 delta present verbatim after promotion
  (`grep -n "DOM-14" docs/specs/01-*.md`, `grep -n "Coalesce on Events"
  docs/agent-context/engineering-principles.md`, etc.)
- skill-shape check: `skills/coalescing/SKILL.md` sections match the
  template order
- link check: every path named in the new files resolves
- first-sweep dry run (task 5) proves the derivation commands in the skill
  actually work against this repo's files

## 8. Independent Review Loop

- Reviewer: a different agent family than the author (per [DOM-11]); Codex
  has been the ecosystem's usual counterparty.
- Reviewer reads: this plan (especially §5), `skills/coalescing/SKILL.md`,
  `docs/coalescing.md`, the DOM spec, `writing-plans.md`,
  `maintaining-traceability.md`, and — for the design source —
  `../engram/docs/specs/10-minimum-memory-model.md` §2–4.
- Review stance: could you run the coalescing sweep confidently and
  correctly from the skill alone, in a repo you have never seen? Are the
  harvest gate and the retired-citation form unambiguous? Does any delta
  contradict existing guidance?
- Author records each finding's disposition in this plan before promotion.

## 8a. Review Findings and Dispositions

Review pass 1 (independent agent, 2026-07-14) — findings on the coalescing
design, each with the author's disposition:

| # | Finding | Disposition |
|---|---------|-------------|
| P0-1 | Half-landed but authoritative-looking: skill and state file exist and nag while [DOM-14] is unpromoted — a soft obligation without a full contract | **Accepted.** Skill and state file now carry `Status: Experimental` until promotion; the session-start obligation is downgraded everywhere to report-and-respond (checked-deferred is first-class); the nag activates only when task 3 lands |
| P0-2 | Plans-tier derivation cannot compute: it assumes the §5.5 status index, which does not exist yet | **Accepted.** Skill step 1 now has an explicit derivation chain (index → `Status:` headers → "not derivable — record blocked, do not guess"); state file marks the plans tier blocked on §5.5; task 5 scopes the first sweep to lessons only |
| P1-1 | Session-start sweep obligation is expensive and easy to game (thin deferrals, "everything is related", never returning) | **Accepted.** Full sweep is its own unit of work — mandatory only on user request, at 2× threshold, or at a completion boundary; checked-deferred must carry the derived counts (a falsifiable artifact, not a checkbox) |
| P1-2 | First sweep would harvest foundation plans that serve as onboarding exemplars | **Accepted.** `exemplar` status added to the index delta; four foundation plans so marked; exemplars exempt until superseded |
| P2-1 | Hard-deleting plan files as the first automation target is aggressive; one missed backlink and you block or delete wrong | **Accepted.** Retirement is now two-step: sweep soft-retires (`retired-pending`, backlinks, ledger); deletion is a dedicated follow-up after second-agent or user verification of the harvest gate |
| P2-2 | "Grep for the theme term" pretends theme clustering is mechanical; it is the judgmental core | **Accepted.** Promotion trigger reframed as an attention signal; skill gains same-theme vs. not-a-theme examples |
| P2-3 | "Fold SHA is the commit you are about to make" breaks under deferred-commit sessions; cues stay broken for days | **Accepted.** Two-phase cue: `folded-in-worktree: <date>, SHA pending`, amended at the next committed state; a cue must not stay pending past the next commit |
| P2-4 | Editing a golden rule in place silently changes what "Golden Rule N" means across SHAs | **Accepted.** Revision marker required: `(revised YYYY-MM-DD; was: <gist>)` — added to the skill and the §5.2 principle text |
| P3-1 | Init-log counts risk duplicate distillation (2026-04-07 entries already live as Golden Rules) | **Accepted.** Task 5 requires dedup against existing rules; fold-as-pointer for already-distilled entries |
| P3-2 | Consumer repos need different thresholds (mm at lessons=10 would nag permanently) | **Already covered / sharpened.** Thresholds are per-repo declared values; propagation task now names calibration explicitly |
| — | Checked-deferred as first-class is the design's best stress test | Agreed — it is now also the *required* first response in the unpromoted state |

Review pass 2 (independent agent, 2026-07-14) — findings and dispositions:

| # | Finding | Disposition |
|---|---------|-------------|
| 2-1 | Session-start rule exceeds task authority: even a checked-deferred line is a mutation outside the user's request scope | **Accepted.** The trigger check is now read-only everywhere (invariants, DOM-14, skill, state file); all coalescing writes happen only inside an authorized maintenance task. Guidance cannot broaden the authority of the current request |
| 2-2 | The fold SHA is impossible: a commit cannot contain its own hash, and the deleting commit does not contain the raw material | **Accepted — factual defect.** Cue is now `source_sha`, a pre-fold commit verifiably containing the raw material, known before editing; the fold commit is optional run-log metadata, never the cue. This also dissolves most of the pass-1 `SHA pending` machinery |
| 2-3 | Destructive coalescing without a commit creates incoherent intermediate state | **Accepted.** Uncommitted sessions are additive-only: draft distillations, propose retirement candidates, delete nothing, advance no watermarks. The destructive phase requires landing authorization |
| 2-4 | Active-plan immutability conflicts with maintaining-traceability's "keep plans current" | **Accepted.** New boundary: task instructions/checklists mutable while active; decision/deviation/review logs append-only; immutable at closure |
| 2-5 | checked-deferred lacks a state model: an unchanged count re-nags every session | **Accepted.** Deferrals now carry `checked_through` (date + SHA), derived counts, reason, and a reconsideration condition; a trip is new only if counts changed or the condition fires |
| 2-6 | Absence of citation is weak deletion evidence; agents follow rules without citing them | **Accepted.** Decay decisions must weigh incidents, coverage, review recurrence, and importance class; citation absence alone never justifies a fold |
| 2-7 | Two-repo fold-up threshold double-counts copied ancestry | **Accepted.** Fold-up requires independent incidents or adaptations with traceable lineage, not two descendants of one inherited rule |
| 2-8 | "Golden rules never decay" should mean "never auto-delete"; rules still need supersession and deprecation | **Accepted.** Importance floor reworded: exempt from automated decay, still subject to explicit revision, supersession, and deprecation with the revision marker |
| 2-9 | Coalesce context projection before storage: most pain is read-tax, not stored history | **Accepted — reorders the plan.** New §5.7 makes the required lessons read "Golden Rules + entries past the watermark"; it is flagged as the highest-value delta in the promotion slice |
| 2-10 | Derivation commands are not mechanically portable to sibling formats | **Accepted.** Propagation task now names format adaptation explicitly; the grep is documented as this repo's shape, not a contract |
| 2-11 | Pilot before propagation | **Accepted.** New task 6: two real sweeps in this repo with a false-positive/context-savings evaluation gate before any propagation |

## 9. Out of Scope

- Adopting Engram itself (it may later become an index over this layer,
  never the source of truth).
- Propagating the deltas to sibling repos (follow-up work; needs the SHA).
- An executable `coalesce-check` script or CI wiring.
- Coalescing specs or implementation docs — those are living documents
  maintained in place per [DOM-6]/[DOM-7], not folded.
- Retiring any of this repo's existing plans (the first sweep decides that,
  gated on harvest).

## 10. Fresh-Eyes Review

Checked before circulating: every touched file is named with its exact edit
point; invariants precede tasks; the harvest gate is enumerated, not vague;
the retired-citation form is spelled out so backstitch behavior is
predictable; thresholds are declared in `docs/coalescing.md` rather than
buried here; nothing in §5 contradicts the uncommitted guidance wave (checked
against the current worktree text of each target file).
