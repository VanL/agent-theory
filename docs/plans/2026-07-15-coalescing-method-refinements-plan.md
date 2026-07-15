# Coalescing Method Refinements — Skill and [DOM-14] Amendment

Class: 5+P — normative spec text ([DOM-14]) is amended (Class 5), and the
change is [DOM-6]-material to how future work is verified and maintained
(the coalescing method), so the process modifier applies. Effective
requirements are `max(5, 5)`'s plus a pre-landing different-family review.
`hardening: N/A — no [DOM-5] risky trigger` (docs/guidance change; no async
or deferred work, no contract/storage/CLI surface, no persistence lifecycle,
no one-way door — the spec delta is a reversible text edit and is not applied
until after review).

Plan type: **spec-authoring** — the [DOM-14] spec text is the primary
normative deliverable, folded up from confirmed method refinements in the
sibling consumer repos (mm, weft). A companion amendment to
`skills/coalescing/SKILL.md` lands in the same wave. No shipped code cites
the touched spec sections, so promotion uses **strategy D**
(`writing-plans.md` §4c/§4d).

## 1. Goal

Promote one week of confirmed coalescing-method refinements — observed and
exercised across the mm and weft consumer repos — into this repository's
canonical coalescing skill, and, where the refinement is normative, into
[DOM-14]. These are refinements to an existing method, not a rewrite: the
skill amendments integrate into the steps where each belongs, and the
[DOM-14] delta touches exactly three existing bullets (trigger, verification,
decay/importance-floor). Nothing rewrites [DOM-14]'s section.

## 2. Source Documents

Source specs:

- `docs/specs/01-development-documentation-operating-model.md` [DOM-14]
  (the amendment target), [DOM-15] (class rules)

Governing method + method state:

- `skills/coalescing/SKILL.md` (the skill being amended)
- `docs/coalescing.md` (this repo's coalescing state; fold-up tier)
- `docs/agent-context/runbooks/writing-plans.md` §4b–4d (spec-delta and
  promotion-strategy machinery)

Evidence lessons (this repo, 2026-07-15):

- `docs/lessons.md` — three-tier verification; framework-fact decay;
  runbook-examples-are-claims entries

## 3. Context and Key Files

Files to modify in this amendment wave:

- `skills/coalescing/SKILL.md` — six integrated amendments (already drafted
  in the working tree; see §6 inventory)
- `docs/coalescing.md` — fold-up tier updated (already drafted): the two
  [DOM-14]-graduating candidates marked accepted-pending-review
- `docs/plans/README.md` — status-index row for this plan (drafted)
- `docs/specs/01-development-documentation-operating-model.md` [DOM-14] —
  the three-bullet delta in §5 below, **NOT yet applied** (promotion is the
  post-review spec-promotion slice)

Read first, and the load-bearing behavior to understand before editing:

- [DOM-14] bullets (lines ~301–334): the trigger bullet
  ("event-derived … never stored"), the two-phase verification bullet
  ("distill, verify links and cues, then retire"), and the
  decay/importance-floor bullet ("recent or still-cited raw material stays
  verbatim … importance floor"). The delta amends these three in place; it
  must not renumber or restructure the requirements list.
  - Comprehension check: which existing bullet already carries the
    importance-floor exemption, and why does the framework-fact clause
    attach to *that* bullet rather than creating a new one? (Answer: the
    decay/importance-floor bullet — framework-fact expiry is a decay
    sub-class, so it belongs beside the other decay guardrails.)
- `SKILL.md` step 1 (trigger derivation), step 2 items 3 and 6 (verify /
  decay), step 4 (promotion/extraction), step 6 (close/land) — each
  refinement is inserted into the step that already owns that concern.

## 4. Invariants and Constraints

- **Minimal delta.** [DOM-14] keeps its structure; only three bullets
  change, each by amendment, not replacement of the surrounding list.
- **Skill voice and order preserved.** No reorganization of `SKILL.md`;
  amendments are integrated into existing steps.
- **Spec tree is canonical after promotion.** The delta in §5 is the
  review target now and the implementation target after the spec-promotion
  slice. Do not treat this plan's appendix text as a second governing
  contract once the delta lands.
- **The [DOM-14] graduation of each refinement requires two independent
  lineages** (the fold-up threshold in `docs/coalescing.md`: 2 independent
  incidents/adaptations). This invariant is the reason the framework-fact
  flag below is load-bearing, not cosmetic.
- **Nothing lands until the different-family review runs.** This plan
  produces drafts only; the orchestrator runs the review and lands.

## 4a. Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## 4b. Spec Baseline

- `5b990ad` — `docs/specs/01-development-documentation-operating-model.md`
  at plan authoring time. Spec-authoring plan: the delta below is applied
  to the spec tree in the post-review spec-promotion slice; the promotion
  baseline identifier is recorded then.
- Promotion applied 2026-07-15 (trigger bullet only, per review): baseline
  `5b990ad` unchanged between authoring and promotion — verified by
  re-reading the target bullet before the edit.

## 5. Proposed Spec Delta

Promotion strategy (see `writing-plans.md` §4d):

| Spec file | Strategy | Sections touched |
|-----------|----------|------------------|
| docs/specs/01-development-documentation-operating-model.md | D — spec-authoring / clarification (no shipped code cites these bullets; land as active text) | [DOM-14] trigger bullet, verification/two-phase bullet, decay/importance-floor bullet |

**Post-review outcome (2026-07-15, grok round — see §10):** only the
**trigger bullet** promoted. The verification and decay bullets are **held
skill-only** (single-lineage; review F2/F3) — their blocks below stay as the
drafted record of what was proposed, marked HELD. They re-enter promotion
when a second independent lineage exists.

Each block below is a **replacement** of one existing [DOM-14] bullet. The
surrounding list is unchanged.

### [DOM-14] — replace the trigger bullet ("coalescing triggers are event-derived …") — PROMOTED 2026-07-15

> - coalescing triggers are event-derived, not calendar-based: counts are
>   computed from the watermark and the current tree, never stored, and are
>   **denominated in the repository's fold unit** — a domain-grouped ledger
>   counts per section, not repo-wide — counting only fold-eligible (cold,
>   unfolded) material; the fold unit and its matching progress model are
>   declared in the repository's `docs/coalescing.md` (per-section
>   watermarks for domain-grouped ledgers; a fold-records index, not a date
>   cursor, for ledgers folded by theme-cluster across dates, since a date
>   cursor falsely claims older unfolded material behind it was folded)

(Review F7 tighten applied before promotion: the fold unit and progress
model are *declared in the state file*, giving the clause an owner and a
verification surface — the derivation command must match the declaration.)

### [DOM-14] — replace the two-phase verification bullet ("coalescing is two-phase and additive-first: distill, verify links and cues …") — HELD skill-only (review F3/F8; single-repo lineage)

> - coalescing is two-phase and additive-first: distill, verify, then
>   retire. Verification spans links, cues, and the distillation's own
>   claims — text fidelity, symbol liveness, and, whenever a distillation is
>   phrased as a present-tense behavior claim, **behavioral parity**
>   reproduced against the code; a fold that touches a runbook or spec also
>   re-verifies the pre-existing examples adjacent to its edits. Every fold
>   leaves a retrieval cue — the date range plus a `source_sha`, a pre-fold
>   commit that verifiably contains the raw material — in the surviving
>   summary or ledger line. The fold commit may be recorded in the run log
>   after it exists, but it is never the cue

### [DOM-14] — replace the decay/importance-floor bullet ("recent or still-cited raw material stays verbatim …") — HELD skill-only (review F2/F6; second lineage not met)

> - recent or still-cited raw material stays verbatim; a lesson encoding an
>   **upstream framework fact** carries a version-bound decay clock — when
>   the pinned dependency makes the violation loudly impossible (a removed
>   API, an import that now raises) it has expired and folds to git with the
>   version fact as its cue, no distillation owed; golden rules and safety
>   invariants carry an importance floor — exempt from automated decay,
>   changed only by explicit revision, supersession, or deprecation with a
>   `(revised YYYY-MM-DD; was: <gist>)` marker

Rule note (per `writing-plans.md` §4c): each amended bullet codifies method
already exercised in the sibling repos; the evidence and its lineage status
are in §5a, and the framework-fact bullet's single-lineage flag is the
primary review item.

## 5a. Evidence Citations and Lineage Status

Six refinements. After the 2026-07-15 review (§10): **one graduates to
[DOM-14]** (fold-unit trigger denomination — two independent lineages);
five land skill-only, two of them ([DOM-14]-proposed but held) awaiting a
second lineage.

1. **Three-tier fold verification** (skill step 2.3; proposed for the
   [DOM-14] verification bullet — **held skill-only per review F3/F8**).
   Text fidelity, symbol liveness, behavioral parity — the third mandatory
   for present-tense claims. Confirmed at the mm Containers/CI
   behavioral-verification addendum (mm `7bbe4e47d`) and applied across all
   subsequent mm folds (Django/DRF pass 2 `127fd437d`, Testing
   `5e8fb8ca7`, Data/CDB `c6356186a`, Deploy `a9d17383e`). Lineage:
   repeated within mm across many sections — strong, but single-repo. The
   review held the bullet-level [DOM-14] amendment until a second repo pays
   the cost (F8: as a silent global floor it risks stalling mechanical
   agents or inviting fake reproduction).

2. **Runbook / spec examples are claims** (skill step 2.3). Folds re-verify
   pre-existing code examples adjacent to their edits. Confirmed twice in
   mm: the Testing fold's Pattern 2 patch-target fix (`5e8fb8ca7`) and the
   Data/CDB fold's `resolve_component_type_tags` example fix
   (`c6356186a`). Skill-level. (Review F4: the SHAs originally cited here
   were mis-pinned — `c72b9b221` is the DRF-typing rule commit — corrected
   above; both incidents are real and verified.)

3. **Framework-fact expiry (decay sub-class)** (skill step 2.6; proposed
   for the [DOM-14] decay/importance-floor bullet — **held skill-only per
   review F2**). A lesson encoding an upstream framework fact expires when
   the pinned dependency makes the violation loudly impossible; fold to git
   with the version fact as cue, no distillation owed. Still-live framework
   facts scatter to topic docs, never a "conventions" home.
   - Lineage 1 (confirmed): mm Django/DRF pass 2 — `datetime.timezone.utc`
     removed in Django 5.0, pinned 6.0.7 fails loudly. Incident fold:
     mm `127fd437d` ("1 decayed"); disposition/source record:
     mm `712ea5440` (review F5: cite both, they are different commits).
   - Lineage 2 (**disputed — resolved by orchestrator + review**): the
     drafting pass reported weft `8382a4d5` "ran no expiry check, and no
     weft commit exercises a pin bump." **Both claims are factually
     wrong**: weft `57255b83` ("Update deps", 2026-07-14) bumps simplebroker
     5.3.2→5.3.3 and is an ancestor of `8382a4d5`, whose commit message
     records "(b) framework-fact expiry mechanism sound, zero expiries
     fired — SimpleBroker facts re-verified against the 2026-07-14 pin bump
     and all hold." The check ran. But it was a **true-negative** — zero
     expiries fired, no expiry disposition path exercised, no durable local
     method change, and the evidence lived only in the commit message (a
     weft recording gap, patched at this landing). Review disposition (F2):
     a true-negative validates the *check*, not the *phenomenon* — it is
     neither an incident nor a durable adaptation under the fold-up
     threshold's wording, so the [DOM-14] graduation is **held** until a
     second repo executes an actual expiry fold or durably installs the
     expiry disposition path. The hold stands *despite* the check having
     run, not because it did not. The skill amendment (step 2.6) lands on
     the mm lineage.

4. **Fold-unit trigger denomination** (skill step 1; [DOM-14] trigger
   bullet — **PROMOTED per review F7**). Triggers denominated in the repo's
   fold unit, counting only
   fold-eligible (cold, unfolded) material; the watermark/progress model
   must match the fold unit (per-section watermarks for domain-grouped
   ledgers; a fold-records index — not a date cursor — for chronological /
   theme-clustered ledgers).
   - Lineage 1: mm recalibration — per-section, fold-eligible-only
     (mm `3487ec358`; mm's per-section watermark table).
   - Lineage 2 (confirmed): weft's demonstrated date-cursor failure —
     the Watermarks note at weft `8382a4d5` shows a theme-clustered fold
     leaving older unfolded sections behind a would-be date cursor, and
     switches to a `## Fold Records` index instead. **Two independent
     lineages confirmed** — this refinement meets the fold-up threshold.

5. **Catch-all section check** (skill step 4). Before designing an
   extraction for a very large section, verify theme coherence; an
   accretion section is a chronological dumping ground whose fix is
   reclassification + extraction of the genuinely homeless clusters, not a
   mega-runbook. Confirmed at mm's Dependency & Build Management extraction
   (mm `63f87cadb`). Skill-level.

6. **Collision-aware coalescing** (skill step 6). Sweeps running beside
   live concurrent sessions defer rules whose domain is under active
   rework, make only localized additive inserts in contested files, and
   report exact insert regions for selective staging. Confirmed at mm's
   Deploy fold (mm `a9d17383e`, "Coordination note … three localized
   inserts … stage these hunks selectively") and DB fold (mm `dc80aa2b8`).
   Skill-level.

## 6. Skill-Amendment Inventory (drafted in the working tree)

| # | Refinement | SKILL.md anchor | One-line content |
|---|-----------|-----------------|------------------|
| 4 | Fold-unit trigger denomination | Step 1, after the "state file owns the ledger format" paragraph | Denominate the count in the repo's fold unit; count only fold-eligible cold material; progress model (per-section watermark vs. fold-records index) matches the fold unit |
| 1 | Three-tier verification | Step 2, item 3 | Verify the distillation across text fidelity, symbol liveness, and — for present-tense claims — behavioral parity; third tier mandatory for current-behavior claims |
| 2 | Examples are claims | Step 2, item 3 (same paragraph) | A fold touching a runbook/spec re-verifies the pre-existing examples adjacent to its edits — they are status claims too |
| 3 | Framework-fact expiry | Step 2, item 6 | Framework-fact lessons carry a version-bound decay clock; expire when the pin makes the violation loudly impossible; still-live facts scatter to topic docs, never a conventions home |
| 5 | Catch-all section check | Step 4, promotion tier | Before extracting a very large section, check theme coherence; reclassify a chronological catch-all and extract only homeless clusters, never a mega-runbook |
| 6 | Collision-aware landing | Step 6, new item 6 | Beside live concurrent sessions: defer rules under active rework, keep contested-file edits localized/additive, report exact insert regions for selective staging |

## 7. Tasks

1. **Skill amendments** (done in the working tree) — the six integrated
   edits above. Verify: greps in §9.
2. **State: fold-up tier** (done) — mark the two graduating candidates
   accepted-pending-review in `docs/coalescing.md` with lineage status,
   including the framework-fact single-lineage flag.
3. **Plan + index** (done) — this plan and its `docs/plans/README.md` row.
4. **Different-family review** (orchestrator) — review this plan and the
   §5 delta, with the framework-fact single-lineage flag as the top item.
5. **Spec-promotion slice** (orchestrator, post-review) — per the review
   verdict, apply **only the trigger bullet** (with the F7 tighten) to
   [DOM-14]; record the promotion baseline identifier in §4b; update
   `docs/coalescing.md` fold-up rows (trigger denomination accepted;
   framework-fact and three-tier held skill-only).
6. **Run-log line** (orchestrator, at landing) — one fold-up line in
   `docs/coalescing.md` recording what graduated and the source SHAs.

## 8. Testing Plan

Docs/guidance change — verification is by inspection and grep, not runtime.

- The delta is text-only; no test harness. The quality gate is the
  different-family review of the delta plus the §9 greps.
- No mocking; there is no code path. The "proof" is that each amended
  bullet's evidence SHA resolves and its lineage claim survives inspection
  (§5a already records the one that does not).

## 9. Verification and Gates

Per-deliverable greps (run from repo root):

```bash
# Skill amendments present (expect one hit each):
grep -n "Denominate the count in the repo's fold unit" skills/coalescing/SKILL.md
grep -n "across three" skills/coalescing/SKILL.md  # (review F11: "three tiers" wraps across lines)
grep -n "pre-existing code examples adjacent" skills/coalescing/SKILL.md
grep -n "version-bound decay clock" skills/coalescing/SKILL.md
grep -n "chronological catch-all" skills/coalescing/SKILL.md
grep -n "runs beside live concurrent sessions" skills/coalescing/SKILL.md

# Fold-up tier updated:
grep -n "accepted-pending-review" docs/coalescing.md
grep -n "does \*\*not\*\* resolve" docs/coalescing.md

# Plan + index:
test -f docs/plans/2026-07-15-coalescing-method-refinements-plan.md && echo plan-exists
grep -n "2026-07-15-coalescing-method-refinements-plan.md" docs/plans/README.md

# After the promotion slice: trigger bullet landed (expect ONE hit),
# held bullets NOT landed (expect ZERO hits):
grep -n "denominated in the repository's fold unit" docs/specs/01-development-documentation-operating-model.md
grep -cn "behavioral parity\|version-bound decay clock" docs/specs/01-development-documentation-operating-model.md
```

Final gates before landing (orchestrator):

- different-family review complete; the framework-fact single-lineage flag
  explicitly disposed in §10
- if the delta lands, `bin/check-dom15-fixtures` (the repo's structural
  gate) still exits 0 and the traceability/self-corpus check is clean
- run-log line written; fold-up rows advanced per the review verdict

## 10. Independent Review Loop

Reviewer: a different agent family from the author (orchestrator runs the
grok round). Read: this plan, its §5 Proposed Spec Delta, the amended
`skills/coalescing/SKILL.md`, the `docs/coalescing.md` fold-up tier, and the
three 2026-07-15 lessons.

Review stance (recommended prompt in `writing-plans.md` §8), plus the
mandatory top item:

- **Dispose the framework-fact single-lineage flag (§5a item 3).** The
  brief's claimed weft second lineage does not resolve; decide whether the
  [DOM-14] decay-bullet graduation lands on mm-single-lineage strength or is
  held skill-only pending a real second lineage. This is a fold-up-threshold
  question, not a wording question.
- Check each amended bullet stays minimal (no restructuring of [DOM-14]).
- Confirm every evidence SHA resolves in the cited repo and that the
  lineage claims are re-derived per repo, not carried over.

### Review Dispositions

Reviewer: grok (read-only sandbox, 2026-07-15); transcript at the session
scratchpad `amendment-review-out.json`. Verdicts: **(a) skill amendments
PASS-with-changes** (all changes applied below); **(b) [DOM-14] delta FAIL
as a three-bullet package — trigger bullet promotes alone**.

| ID | Severity | Finding (gist) | Disposition |
|----|----------|----------------|-------------|
| F1 | P1 | Plan/state falsely recorded that weft "ran no expiry check" / "no pin bump exists" — the check ran (weft `8382a4d5` commit message) at a real pin bump (weft `57255b83`); evidence was commit-message-only (weft recording gap) | **Accepted.** §5a item 3 and the `docs/coalescing.md` fold-up row corrected to true-negative-with-evidence; weft run-log line patched additively to close the recording gap |
| F2 | P1 | Weft true-negative is not a second lineage under "2 independent incidents/adaptations" — no expiry incident, no durable adaptation | **Accepted.** Decay bullet held skill-only; re-enters promotion on an actual second-repo expiry fold or durably installed disposition path |
| F3 | P1 | Verification bullet smuggles skill-level refinements ([DOM-14] promotion on single-repo lineage) and contradicts §4's own two-lineage invariant | **Accepted.** Verification bullet held skill-only; §5 marked HELD |
| F4 | P2 | §5a item 2 SHAs mis-pinned (`c72b9b221` is the DRF-typing commit; Testing fold is `5e8fb8ca7`, Data/CDB is `c6356186a`) | **Accepted.** Citations corrected in items 1–2 |
| F5 | P2 | Framework-fact lineage cited the disposition commit (`712ea5440`) where the incident fold is `127fd437d` | **Accepted.** Both now cited with roles |
| F6 | P2 | Decay bullet, if ever promoted, lacks check cadence, cue shape, and an impossibility-verification floor | **Accepted as promotion precondition.** Recorded in §5a item 3's re-entry condition; wording work owed at that future promotion, not now |
| F7 | P2 | Trigger bullet: fold-unit declaration had no owner/boundary | **Accepted.** Clause added: fold unit + progress model declared in `docs/coalescing.md`; promoted with the tighten |
| F8 | P2 | Behavioral parity as a silent global floor risks stalling mechanical agents / fake reproduction | **Accepted.** Skill-level only (agents can weigh cost in context); not a DOM floor until a second repo pays the cost |
| F9 | P3 | All six skill edits land in the right steps, voice preserved | Noted; no change |
| F10 | P3 | "Five" vs six amendments count | **Accepted.** Fixed in §3 and §7 |
| F11 | P3 | §9 grep `"three tiers"` doesn't match the wrapped skill text | **Accepted.** Grep changed to `"across three"` |
| F12 | P3 | Fold-up row listed framework-fact co-equal with fold-unit while doubting its lineage | **Accepted.** Row rewritten: one graduate (trigger denomination); framework-fact skill-landed / DOM-held |
| F13 | nit | Step 2.6 wrapping density | **Declined** — pre-existing density; reflow deferred to the skill's next substantive edit |

## 11. Out of Scope

- Applying the [DOM-14] delta (that is the post-review spec-promotion
  slice, not this drafting plan).
- Any change to the sibling repos (mm, weft) — read-only for evidence.
- Recalibrating this repo's own thresholds (`docs/coalescing.md`
  Thresholds table) — the refinements are method, not this repo's numbers.
- Engineering-principles §15 or any surface other than [DOM-14] and the
  coalescing skill.

## 12. Fresh-Eyes Review

Re-read as a new engineer: the delta is three bounded bullet replacements
with exact before/after anchors; the skill edits name their step and
concern; the one weak citation is flagged loudly rather than smoothed over.
No mega-abstraction added — the refinements integrate into existing steps.
The single genuine risk is over-claiming #3's [DOM-14] graduation; §5a and
§10 force that to the review's attention rather than burying it.
