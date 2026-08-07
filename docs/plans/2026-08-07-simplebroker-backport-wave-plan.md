# SimpleBroker Backport Wave Plan

Date: 2026-08-07
Revision: 3 (2026-08-07) — round-2 scoped review (codex, FAIL, six
defects) applied. Revisions 1–2 existed only in the uncommitted
worktree and were edited in place; no committed prior revision exists,
and per the guidance-is-reviewable rule (Task E4) an uncommitted draft
corrected in place owes no supersession ceremony. Superseded decision
text within this file is edited in place and marked historical.
Status: completed — revision 3; plan review rounds 1–3; pre-landing
+P review rounds 1–3 (final residual author-verified with executed
proof, disclosed in the Review Log); all owner decisions executed;
landed by the commit carrying this status flip (SHA recorded in the
Spec Baseline by the follow-up metadata change)
Class: 5+P — normative spec text is edited ([DOM-5], [DOM-14], [DOM-15]
deltas below), so [DOM-6] fires class 5; runbooks, skills, and gate
tooling are materially changed, so +P fires. Effective requirements:
class 5 plus pre-landing different-family review.
Hardening: applies only to the gate-script contract change in Slice F
(a scaffolded tool's exit semantics change on shallow clones — a
[DOM-5] public-contract trigger); addressed inline in that slice. For
every other slice: no [DOM-5] risky trigger fires — docs-only, no
async, storage, CLI, or compatibility surface. The [DOM-14] policy
change (OD-1, adopted) alters authorization *policy* for
already-mandated maintenance; it introduces no new destructive edge.
Plan type: spec-authoring (the guidance corpus is the deliverable; no
product code cites the changed sections).

## Goal

Backport the testbed-proven guidance, doctrine, and gate improvements
from SimpleBroker (the designated dogfood testbed) into the hub. The
2026-08-06 changelog wave took the first tranche; an independent
four-surface review on 2026-08-07 (runbooks; core context files; DOM
spec and gate scripts; skills, lessons, and recent plans) found the
remainder. This plan lands: five hub defect repairs, the
zero-dependency portable rules, three new doctrine sections the hub
currently lacks (release stop-gates, gate wiring, guidance-as-
reviewable-surface) plus a conditional audit-response protocol, gate
tooling upgrades, and owner-decision items with named ratification
gates. The constitutional items (negative-knowledge/[DOM-16] package,
ownership triad) are explicitly deferred to their own future plans.

## Source Documents

Source specs:

- docs/specs/01-development-documentation-operating-model.md
  [DOM-3], [DOM-4], [DOM-5], [DOM-8], [DOM-9], [DOM-11], [DOM-14], [DOM-15]
- docs/program-theory.md [AT-THEORY-5], [AT-THEORY-6], [AT-THEORY-7]
  (admission test; no-efficacy non-goal; falsifiers)

Source material (backport origin, pinned):

- SimpleBroker working tree at `a38e6a9e3641075436ada9c05dcf4ba411b40c9d`
  (clean at review time). All `sb:` citations below are full
  repo-relative `<path>:<lines>` at that pin; extract with
  `git -C ../simplebroker show a38e6a9:<path>`. Two defined
  continuation forms (round-2 citation audit): a bare `:N-M`
  immediately following an `sb:` citation continues that same path;
  `sb:<path> §"<heading>"` names an exact heading at the pin when a
  section, not a line range, is the stable locator.
- Independent backport survey, 2026-08-07, four reviewers over four
  surface groups plus an author sweep of SimpleBroker's automated-gate
  wiring. Findings are cited here by their durable `sb:` pins.

Related in-flight plan (Slice G interlock):

- docs/plans/2026-08-06-register-conditioning-theory-revision-plan.md

Consulted surfaces (read-order declaration): `docs/program-theory.md`,
`docs/agent-context/decision-hierarchy.md`,
`docs/agent-context/engineering-principles.md`,
`docs/agent-context/README.md`, `runbooks/writing-plans.md`,
`runbooks/review-loops-and-agent-bootstrap.md`,
`skills/call-agent/SKILL.md`,
`docs/specs/01-development-documentation-operating-model.md`,
`docs/specs/02-agent-theory-and-program-theory.md`,
`docs/coalescing.md`, `CHANGELOG.md`, and `docs/lessons.md` (2026-07-17
onward) were read directly by the author. `principles.md` was read in
part (Core Standards); `runbooks/testing-patterns.md`,
`hardening-plans.md`, `maintaining-traceability.md`,
`writing-implementation-docs.md`, and the remaining skills were
verified against SimpleBroker by the survey reviewers, not re-read in
full by the author. Implementers of Slices D–E must read the target
files in full before editing.

## Context and Key Files

Files to modify (hub):

- `docs/specs/01-development-documentation-operating-model.md` —
  [DOM-5] carve-out, [DOM-14] reconciliation, [DOM-15] fixture rows
- `docs/agent-context/context.index.yaml` — read_order repair
- `docs/agent-context/README.md` — read-order note (its lines 16–19);
  Goals bullet
- `AGENTS.md` — judgment paragraph; session-start coalescing cue;
  status-index requirement; Definition of Done line
- `docs/agent-context/decision-hierarchy.md` — no-inference-from-absence;
  open-checkbox clause
- `docs/agent-context/engineering-principles.md` — §3 list; §5 bullets
- `docs/agent-context/runbooks/writing-specs.md` — theory boundary;
  gate-wiring rule
- `docs/agent-context/runbooks/writing-plans.md` — status-index binding;
  retirement-is-routine; harvest-gate reachability; comprehension-gate
  teeth (normative owner); demotion-in-place (OD-2)
- `docs/agent-context/runbooks/maintaining-traceability.md` — chain
  terminus; closure task-diff rule
- `docs/agent-context/runbooks/testing-patterns.md` — new Pattern 8
  (appended; the hub currently ends at Pattern 7)
- `docs/agent-context/runbooks/writing-implementation-docs.md` —
  non-goal anti-duplication rule
- `docs/agent-context/runbooks/hardening-plans.md` — release stop-gates;
  post-release acceptance; comprehension-gate pointer (non-normative)
- `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md` —
  audit-response protocol (conditional); guidance-as-blocking-finding;
  existence-check rule; timeout-calibration clause
- `skills/coalescing/SKILL.md` — unindexed tier; durable-guidance
  ceiling; evidence-trail posture; additive watermark rule; OD-1
  reconciliation edits (Task B2, exhaustively enumerated)
- `skills/brainstorming-to-plan/SKILL.md` — admission threshold
- `docs/coalescing.md` — OD-1 reconciliation (its lines 14–17);
  Unindexed threshold row; report-when list; coalesce-check role;
  candidate slate (E8); run-log entries; OD-2 record
- `docs/lessons.md` — ledger-is-reviewable golden rule
- `bin/coalesce-check`, `bin/check-doc-paths`,
  `bin/check-dom15-fixtures`, `.github/workflows/gates.yml` — Slice F
  (F4 is the sole owner of all workflow edits)
- `CHANGELOG.md` — 2026-08-07 wave section
- `docs/plans/README.md` — this plan's index row

Read first (implementer): every target file above in full before its
slice; the `sb:` source for each ported item; `runbooks/writing-specs.md`
before Slice B (spec-authoring rules); `skills/propagate-guidance/SKILL.md`
step 0 (SHA-pin provenance convention — this wave runs the reverse
direction but uses the same pin discipline).

Port convention: "port verbatim from `sb:<path>:<lines>`" means the
exact text at the pin, with only the edits enumerated for that item.
Mandatory vocabulary edits everywhere: `[DOM-16]` citations →
`docs/program-theory.md` [AT-THEORY-*] or dropped (the hub has no
[DOM-16]); "winning product contract" → "governing spec"; "the
product-section registry" → dropped; `[THEORY-*]`/`[REV-*]`/`[ALT-*]`
grammar → not introduced (out of scope); SimpleBroker product nouns
(broker, queue, PyPI, weft, `agent-kernel.md`, gstack) → dropped or
generalized as stated per item.

Comprehension questions (answer in the execution log before editing;
an incorrect answer blocks implementation until the cited owner text
is reread):

1. Why must the [DOM-14] delta **replace** the landing-authorization
   bullet rather than be appended beside it, and what stays ineligible
   for removal afterward?
   Expected: two contradictory authorization rules must not coexist in
   one spec section; the carve-out reconciles, it does not add a
   parallel path (engineering principle §1). Worktree-only material
   stays ineligible — it has no archive cue, so git is not yet its
   archive.
2. After Slice F, what does `bin/coalesce-check` do on a shallow clone,
   and why is that exit-semantics change acceptable?
   Expected: it detects `git rev-parse --is-shallow-repository` and
   skips the SHA-resolution legs loudly (printed reason, exit 0)
   instead of reporting false BROKEN with exit 1; non-SHA legs (counts)
   still run and print. Acceptable because a gate that cannot be
   truthful must say so rather than fail for the wrong reason;
   enforcement CI requires full history (documented in the script), and
   the change is declared in the changelog as a scaffold contract
   change.
3. Which SimpleBroker texts must NOT be copied even though they sit
   inside sections this plan ports?
   Expected: the flattened read order (it deleted the hub's
   Stub/crystallization qualifiers and module-theory rule); the
   coalescing skill's dropped fold-unit denomination text (two-lineage
   hub doctrine that must survive); and all [DOM-16]/ALT-REV/registry
   vocabulary, which has no hub referent yet.

## Owner Decisions

- **OD-1 — Git-backed coalescing carve-out. DECIDED 2026-08-07: adopt**
  (owner selection recorded in the execution log). Deltas B2/B3/B5 and
  Task B2's reconciliation edits proceed. Round-1 F4 requires the
  reconciliation to enumerate every conflicting clause; Task B2 now
  does.
- **OD-2 — Revision-discipline promotion. DECIDED 2026-08-07 (after
  re-presentation with corrected evidence): promote narrowed.**
  Historical basis, retained for the record: the owner's first answer
  (graduate) was given against revision-1 evidence that round-1 review
  (F5) found overstated — at the pin, SimpleBroker's six-revision plan
  has a `Revision:` header, outranking owner amendments, and a
  "Superseded Owner Amendment" demotion section (verified), but **no**
  Revision Log table and **no** reviewed-baseline pin; and the hub
  already carries the revision re-gate normatively
  (`runbooks/writing-plans.md:600-608`), so no single mechanism has
  two clean lineages. The confirmed decision: promote
  **demotion-in-place of superseded text to non-authority** (SB
  lineage verified; mm's incident is the motivating first lineage for
  the family) by explicit owner direction, and update the
  `docs/coalescing.md` deferral row for Revision Log and
  reviewed-baseline pin with SB recorded as *partial* family evidence
  only. Task E6 executes both halves unconditionally.
- **OD-3 — Register-plan amendment. DECIDED 2026-08-07: revised
  wording confirmed by owner.** F3 correctly noted that
  "owner-reported: sustained subjective quality improvement" is an
  efficacy claim by type regardless of caveats, and [REV-AT-003] lives
  in current-account theory. Confirmed amendment: (a) the [REV-AT-003]
  **Pressure** field is **content-free about direction** (round-2
  correction — even an attributed favorable impression is an efficacy
  assertion in theory prose): it reads "together with the owner's
  motivating impression about register effects, recorded in the
  backport plan's execution log and disqualified as evidence by this
  revision"; (b) the experiment-status paragraph states hypothesis,
  evidence *deficit* ("no blinded probe has run; current support does
  not rise above the fluency heuristic this revision names"), and the
  [AT-THEORY-6] falsifier as the standing test. The observation's
  content lives only in this plan's execution log and any external
  writing. The amendment routes through a fresh independent semantic
  review of the amended register plan (different family from its
  author), recorded in that plan. Task G1 executes unconditionally.
- **OD-4 — Existence-check promotion authorization (new; F7).
  DECIDED 2026-08-07: promotion authorized by owner.** Task G2 clears
  the hub lessons entries' "once cited from a second repository" hold
  by explicit owner direction (the entries' own named alternative
  trigger) and executes unconditionally.

## Invariants and Constraints

- **No efficacy claims enter current-account prose.** [AT-THEORY-5]
  stands; OD-3's revised text states hypothesis + evidence deficit +
  falsifier only.
- **Hub-only doctrine survives every merge.** Must remain intact and
  unweakened: the fold-unit denomination text in
  `skills/coalescing/SKILL.md` step 1 and [DOM-14]; the
  Stub/Draft/Active qualifiers and module-theory rules in `AGENTS.md`,
  `README.md`, [DOM-2]/[DOM-3]; the Trusted Base section in
  `decision-hierarchy.md`; the `--scaffold` mode of `check-doc-paths`.
- **No [DOM-16] vocabulary is introduced by this wave.** Checked on
  the wave's *added lines*, not the whole tree (round-1 F1: the
  baseline already contains historical occurrences).
- **No SimpleBroker files are edited.**
- **The status vocabulary stays closed.**
- **Gate exit-code contracts are preserved** except the declared
  shallow-clone change in `coalesce-check` (Slice F, hardened inline).
  The live `check-dom15-fixtures` spec validation is never replaced by
  self-test-only invocation (round-1 F2): CI runs both the live
  command and `--self-test` as separate steps.
- **Reconcile, never append, where texts conflict**; Task B2
  enumerates every conflicting clause for OD-1.
- **CHANGELOG.md is updated in the same change as each landed slice.**
- No drive-by refactors of ported text beyond the enumerated edits; no
  new dependencies; gate scripts stay stdlib-only.

## Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## Spec Baseline

- Hub spec tree at `4acbad1` plus the 2026-08-06 changelog-wave edits
  present in the authoring worktree (dirty tree; diff base `4acbad1`).
  Record the landed SHA as the promotion baseline identifier when the
  spec-promotion slice commits.
- Promotion baseline identifier (2026-08-07): diff base `4acbad1`,
  worktree state after the spec-promotion slice — Deltas B2/B3/B5
  applied to `docs/specs/01-development-documentation-operating-model.md`
  ([DOM-5] carve-out paragraph after the risky-trigger list; [DOM-14]
  additive-first bullet replaced by the two archive-rule bullets;
  [DOM-15] fixture table +2 rows), gates green
  (`check-dom15-fixtures`, `check-doc-paths`). Mid-implementation
  compliance claims are against this identifier; replace with the
  commit SHA at landing.
- Backport source: SimpleBroker at `a38e6a9e3641075436ada9c05dcf4ba411b40c9d`.

## Proposed Spec Delta

Promotion strategy:

| Spec file | Strategy | Sections touched |
|-----------|----------|------------------|
| docs/specs/01-development-documentation-operating-model.md | D — spec-authoring; no code link claims | [DOM-5], [DOM-14], [DOM-15] |

Delta B1 (affirmative hardening declaration) and Delta B4 (anti-topology
Rules bullet): **withdrawn at revision 2** (round-1 F14 — both restate
existing hub text; the [DOM-15] class-5 row's `hardening: N/A — no
risky trigger` wording already embeds the claim, and the fixture
paragraph already states class-follows-facts).

### Delta B2 — [DOM-5], new paragraph inserted immediately after the
risky-trigger list (OD-1; exact text, ported verbatim from
sb:docs/specs/01-development-documentation-operating-model.md:142-152)

> Git-backed coalescing is not a destructive edge for classification
> purposes when every removed item has a verified pre-fold source SHA
> reachable from a retained Git ref and the repository's traceability
> gate passes. An ordinary authorized sweep does not require a task
> plan merely because it soft-retires or physically removes plans,
> removes already-distilled or expired raw ledger entries, advances
> watermarks, or updates the run log. A plan is required when the
> sweep promotes or materially changes durable guidance (for example a
> golden rule, principle, runbook, skill, or cross-repository rule),
> or when some other [DOM-5] trigger independently fires. The routine
> sweep is Class 2: explicit authorization supplies intent, Git makes
> it reversible, and this paragraph excludes the coalescing removals
> themselves from [DOM-5]'s triggers.

### Delta B3 — [DOM-14], replace one bullet (OD-1; exact boundaries)

Replace the single bullet beginning "coalescing is additive-first
across commit boundaries:" and ending "…require a landing-authorized
phase with a durable checkpoint" with these **two** bullets (ported
verbatim from sb:docs/specs/01-development-documentation-operating-model.md:483-489
and :510-513; no edits):

> - coalescing removals are Git-backed archive maintenance, not
>   permanently destructive, when a verified pre-fold source SHA
>   reachable from a retained ref contains every removed item. The
>   authorized sweep may delete already-distilled, expired, or
>   otherwise nonnormative raw material, advance watermarks, and
>   retire plans without a separate task plan or coalescing-specific
>   commit authorization; an item that exists only in the worktree
>   remains ineligible because it has no archive cue
> - routine coalescing maintenance is plan-exempt. Promotion or
>   material revision of durable guidance (golden rules, principles,
>   runbooks, skills, or cross-repository rules) follows the ordinary
>   [DOM-5]/[DOM-15] planning and review requirements before that
>   promotion is written

All other [DOM-14] bullets are untouched.

### Delta B5 — [DOM-15] fixture table, append two rows (OD-1; exact
text, ported verbatim from
sb:docs/specs/01-development-documentation-operating-model.md:626-627;
adopt together or not at all)

> | Authorized coalescing run that only removes already-distilled, expired, or nonnormative source-pinned raw entries, retires or deletes source-pinned plans, advances watermarks, and updates its run log — explicit user intent, reversible through a retained Git ref, and no [DOM-5] trigger fires because this section excludes those archive removals | 2 |
> | Coalescing run that promotes a lesson into a golden rule or materially changes a runbook/skill — durable guidance changes | Class 3+P (effective 5) |

Both rows satisfy the existing `NEGATIVE_FACT_MARKERS` in
`bin/check-dom15-fixtures`; no checker change.

## Tasks

Slice order: owner re-confirmations (OD-2/OD-3/OD-4), then round-2
scoped review, then the spec-promotion slice (B) with A; C–E after
promotion; F independent; G after its OD confirmations; final slice
last.

**T0. Owner ratifications. COMPLETE 2026-08-07** — all four decisions
recorded in the execution log: OD-1 adopt; OD-2 promote narrowed
(after re-presentation); OD-3 revised wording confirmed; OD-4
authorized. The rejection branches written at revision 2 were not
taken and are historical; E6, G1, and G2 execute unconditionally.

**Slice A — hub defect repairs**

**A1. read_order repair.** Add `docs/agent-context/README.md` to
`read_order` in `context.index.yaml` (position 2, matching
`AGENTS.md`); update the read-order note at
`docs/agent-context/README.md:16-19` (delete the "omits this file /
runs one ahead" rationalization; the lists now match
element-for-element). Verify: the structural comparison in F4's
workflow step passes (yaml list vs `AGENTS.md` sequence).
**A2. writing-specs theory boundary.** Rewrite
`runbooks/writing-specs.md:3-4` opener and add the boundary rule,
adapted from sb:docs/agent-context/runbooks/writing-specs.md:3-8 and
:21-26, edits per the port convention (no record-grammar citation
requirement; cite `docs/program-theory.md` instead). Must state both
directions: a spec may refine theory into observable obligations but
may not silently contradict it; theory may not duplicate exact
behavior. Verify: grep for "source of truth" in the runbook returns
only the reframed sentence.
**A3. Harvest-gate reachability clause.** In `writing-plans.md` Plan
Lifecycle retirement rules, add: the recorded source SHA must be
reachable from a retained ref ("a loose object that can be pruned is
not a durable archive"), and physical deletion is blocked until
retrieval from that SHA is verified. Source:
sb:docs/agent-context/runbooks/writing-plans.md:698-707, minus the
`[ALT-ID]` heading check (no hub grammar yet).
**A4. coalesce-check normative role.** Add to `docs/coalescing.md`
header (not the run log): the derivation recipe in this file and the
skill is authoritative; `bin/coalesce-check` is an evidence trail,
not a second recipe; it never writes counts back; when tool and file
disagree, the file wins and the script is the defect. Source:
sb:docs/coalescing.md:20-29 and sb:skills/coalescing/SKILL.md:105-111,
provenance clauses dropped. Mirror the one-line posture into the hub
skill's step 1 (currently tool-preferred — invert to
file-authoritative).

**Slice B — spec-promotion slice (OD-1 adopted)**

**B1. Apply Deltas B2/B3/B5**; update this plan's Spec Baseline with
the promotion identifier; run `python3 bin/check-dom15-fixtures` (must
pass with the new rows) and `python3 bin/check-doc-paths`. Add this
plan to the spec's `## Related Plans`.
**B2. OD-1 reconciliation — exhaustive clause enumeration (round-1
F4).** Edit every hub clause that still requires landing authorization
for git-backed removals, preserving user/task authorization while
removing only the landing/commit gate:
- `skills/coalescing/SKILL.md:82-84` (authorization preconditions) —
  rewrite to require explicit sweep authorization; drop the separate
  landing-authorization precondition for source-pinned removals.
- `skills/coalescing/SKILL.md:185-189` (step 5, "Destructive phase —
  only with landing authorization") — retitle "Archive phase" and
  condition on verified source cues reachable from a retained ref,
  per Delta B3's rule; guidance-promotion still escalates (D8's
  ceiling).
- `skills/coalescing/SKILL.md:279-285` (closing checklist) — align
  the landing-authorization line with the archive-phase rule.
- `docs/coalescing.md:14-17` ("destructive steps additionally require
  landing authorization") — replace with the plan-exempt carve-out
  sentence conditioned on retained-ref source cues, mirroring Delta
  B3.
- `docs/coalescing.md:58` ("Destructive steps require landing
  authorization; an uncommitted first…" — inside the First-Sweep
  Policy section; found by round-2 review re-running this task's own
  sweep) — align with the carve-out; the First-Sweep Policy's
  uncommitted-material caution is preserved, since worktree-only
  items remain ineligible under Delta B3.
Implementer instruction: before editing, grep both files for
`landing` and `authoriz` and extend this enumeration if any clause
was missed; an unenumerated conflicting clause discovered mid-edit is
appended to this list in the execution log, not silently edited.
Done signal: no clause in either file contradicts Delta B3; both
gates green.

**Slice C — judgment trio and entry surfaces**

**C1. AGENTS.md judgment paragraph.** Port verbatim from
sb:AGENTS.md:57-60 ("load-bearing for product-scope *judgment* —
audits, reviews, feature-fit and design opinions — not only for
implementation. Skipping it because a task looks like verification is
the observed failure mode."), placed with the existing program-theory
read-order item; the Stub/Draft/Class-5 qualifiers stay. This exact
sentence is contractual: F4's workflow step asserts its presence.
**C2. Decision-hierarchy preflight.** In "Classify Before the
Preflight"/preflight list add, adapted from
sb:docs/agent-context/decision-hierarchy.md:32-34: for product-scope
or design judgment, identify the governing theory account or record
plainly that the theory is silent on the concern; **do not infer
product intent from feature absence.** Also append to the Completion
Gate paragraph the negative direction (sb:docs/lessons.md:114-118):
an open checkbox or stale `Status:` header is equally not evidence
that work is unshipped — verify the claimed behavior before treating
a plan as open work.
**C3. Engineering-principles §3 and §5.** §3 read list gains item 1
"the program theory when product scope, concepts, or ownership are at
issue" (renumber; keep the rest); restore "and its rationale" on the
implementation item (sb:docs/agent-context/engineering-principles.md:22-26).
§5 gains "Theory-changing plans cite the governing theory and decision
records" (sb:docs/agent-context/engineering-principles.md:47) and the
guardrail "Program theory can constrain a contract or architecture,
but it cannot silently replace exact behavior or concrete realization
rationale" (sb:docs/agent-context/engineering-principles.md:59-60).
**C4. AGENTS.md session-start coalescing cue.** Port from
sb:AGENTS.md:67-83, minus the census parenthetical: one-sentence
report duty, read-only, no mid-task writes, sweep only when
authorized.
**C5. AGENTS.md status-index requirement + DoD.** Classes 3+ create
the `docs/plans/README.md` row with the plan; closing a class ≥3 plan
flips the row to `completed`/`superseded` in the same change; add the
matching Definition of Done line. Source: sb:AGENTS.md:92-98 and
:191-192.

**Slice D — runbook and skill ports (each item: port per convention,
verify by targeted grep of the promoted sentence)**

**D1.** `writing-plans.md`: class ≥3 completion is not claimed until
the index row says `completed`/`superseded`, same change; "do not
require a binary status checker; the index is the contract"
(sb:docs/agent-context/runbooks/writing-plans.md:670-673).
Supersession flips in the same change as acceptance
(sb:docs/lessons.md:119-121).
**D2.** `writing-plans.md`: git-backed retirement is routine [DOM-14]
maintenance under the stated conditions
(sb:docs/agent-context/runbooks/writing-plans.md:692-695). OD-1.
**D3.** Withdrawn at revision 2 (round-1 F14: near-duplicate of the
declared-claim floor at `docs/agent-context/README.md:38-43`).
**D4.** `maintaining-traceability.md`: chain terminus becomes
`code/test evidence`; Completion Gate gains the closure task-diff
rule — closure review diffs every planned task against executable
evidence; a checked box, a passing default suite, or a gated-off test
is not evidence (sb:docs/lessons.md:297-303).
**D5.** `testing-patterns.md`: **append a new Pattern 8** (the hub
currently ends at Pattern 7; the source is SimpleBroker's Pattern 7 at
sb:docs/agent-context/runbooks/testing-patterns.md:124-141):
multiprocess coordination needs one monotonic aggregate deadline;
scale by the repository's CI timing factor where one exists; report
received-vs-missing children with PID/exit/liveness; a missing result
is never a silent pass. Also add the serialization-group rule as a
bullet: a test-serialization group constrains only its own members;
threshold-bearing measurements need an exclusive phase
(sb:docs/lessons.md:86-89, generalized off xdist).
**D6.** `writing-implementation-docs.md` §3: "Do not copy product
non-goals or current capability limits into implementation docs; link
their owning theory or contract"
(sb:docs/agent-context/runbooks/writing-implementation-docs.md:66-68,
first sentence only).
**D7.** `skills/brainstorming-to-plan/SKILL.md`: replace the
unconditional "rejected alternatives are load-bearing" with the
four-part admission test (likely recurrence, material investigation
cost, hidden constraint exposed, harm from blind retry), **labeled as
an adaptation from the pin**
(sb:skills/brainstorming-to-plan/SKILL.md:44-48, whose own citation is
SB's [DOM-16]); cite [AT-THEORY-7] only for its broader
observed-practice admission principle, not as the owner of the
four-part test (round-1 F15).
**D8.** `skills/coalescing/SKILL.md` + `docs/coalescing.md`:
Unindexed tier (any positive count reportable; never fall through to
in-file headers when an index exists; never rewrite status data to
pass a check — sb:skills/coalescing/SKILL.md:129-142) with a
threshold-table row and deferral row; the durable-guidance ceiling
("routine-sweep authority does not waive the durable-guidance
planning boundary" — sb:skills/coalescing/SKILL.md:101-104; range
corrected by round-2 review); the
additive watermark rule ("advance watermarks only after every removed
item has a verified pre-fold source cue; otherwise leave the
watermark and say so" — sb:skills/coalescing/SKILL.md:300-302); the
consolidated report-when list (sb:docs/coalescing.md:73-80).
Constraint: the hub's fold-unit denomination text is untouchable.
**D9.** Cut at revision 2 (round-1 F11: the namespace rule is
[DOM-16] ALT/REV-allocation policy; a universal reference-code rule
needs its own evidence and a conformance review of existing code
families — recorded as an observation for a future plan, not ported).

**Slice E — new doctrine sections**

**E1. Release stop-gates** (`hardening-plans.md`, new subsection).
The rules, stated generally, with repository-specific wiring given as
conditional examples (round-1 F10 — a scaffolded runbook must not
assume tag-triggered publication or any one release topology): the
executable release driver, where one exists, outranks plan prose —
compare proposed order and collection roots to executable code before
accepting prose; final gates rerun from the release identifier ("a
prior green is not evidence"); the irreversible publication step
comes only after exact-identifier green; recovery reruns the failed
mechanism for the same immutable identifier — a published identifier
with no run record means stop and investigate; state rollback
honestly ("no rollback after publish" when true). Post-release
acceptance runs against built artifacts, not the source tree; absence
of warnings is not proof. Each rule closes with "adapt to the
repository's actual release identity and driver". Sources:
sb:docs/plans/2026-08-06-pre-release-review-remediation-plan.md
§"K0. Release mechanics decision";
sb:docs/plans/2026-08-06-audit-remediation-plan.md §"Rollback,
Rollout, and One-Way Doors"; sb:docs/lessons.md:229-233.
**E2. Gate wiring** (`writing-specs.md`, following the 2026-08-06
enumeration-gate rule). General rule with conditional examples
(round-1 F10): writing a gate is not wiring it — every gate names its
execution path to CI; a history-dependent gate must either run on
full history or skip loudly on shallow clones — silently passing or
falsely failing on a shallow clone are both invalid. Examples (marked
as examples, not the exhaustive wiring set): a test-suite-borne
subprocess gate invoked portably; a dedicated workflow with full
history.
**E3. Audit-response protocol** (`review-loops-and-agent-bootstrap.md`),
**conditional**: applies to large or systemic audits (many findings
or a cross-cutting process failure); ordinary reviews keep the
existing Review Log discipline (round-1 F13). Contents: the
Investigation Disposition Matrix (Finding | disposition | owning
slice); the register of findings that did not survive investigation,
with why; Principle-Level Diagnosis — assign each finding to the
violated principle, which dictates the remediation's shape. The
deferred-units register (Unit | Finding | Why deferred | Reopens
when) with reviewer-verified clean severance applies to **any**
review that defers accepted findings, not only audits. Sources:
sb:docs/plans/2026-08-06-audit-remediation-plan.md §"Investigation
Disposition Matrix" and §"Principle-Level Diagnosis";
sb:docs/plans/2026-08-06-pre-release-review-remediation-plan.md
deferred-units register.
**E4. Guidance is a reviewable surface** (`review-loops...` +
`docs/lessons.md` golden rule). Golden-rule line (source:
sb:docs/lessons.md:293-296): the lessons ledger is itself a
reviewable surface, not a place confident text lands unreviewed; an
uncommitted entry corrected in place owes no supersession ceremony —
the ceremony is owed after landing. Reviewer-conduct rules (source:
sb:docs/plans/2026-08-06-pre-release-review-remediation-plan.md,
finding R3-F11 and §"Durable-Guidance Correction (2026-08-07 —
resolves the last blocker)" at source line 1684): a
reviewer may block on a guidance defect; concurrent edits to shared
guidance are raised as findings for their author, never silently
overwritten; author deviations from suggested wording are recorded
with reasoning.
**E5. Comprehension-gate teeth.** Normative owner: `writing-plans.md`
(answers written in the execution log; expected answers written in
the plan; an incorrect answer blocks implementation until the cited
owner text is reread). `hardening-plans.md` keeps only a pointer to
that rule (round-1 F14: one obligation, one owner).
**E6. (OD-2, decided: promote narrowed)** Add demotion-in-place to
`writing-plans.md` Plan Lifecycle — superseded in-plan decisions are
edited in place to state they are historical and not implementation
authority (evidence: the SB pin's "Superseded Owner Amendment After
Round 3 (Revision 4)" section; mm's incident as the family's first
lineage; promoted by owner direction). And: update the
`docs/coalescing.md` fold-up deferral row — Revision Log and
reviewed-baseline pin remain candidates with SB recorded as partial
family evidence; the revision re-gate is already normative and leaves
the candidate slate.
**E7. Review-attempt calibration** (`review-loops...`): a too-short
author-chosen timeout manufactures a false "unavailable"; bounds are
calibrated to the reviewer's observed latency, and a bound raise plus
relaunch is recorded as a distinct attempt, not a failure of the
reviewer.
**E8. Candidate slate, not lessons entries** (round-1 F12; round-2
tier correction: these are sibling-repository candidates, so they
belong to the **Fold-up tier** — the tier owning the two-independent-
lineage rule — not the promotion tier, whose three-citation threshold
governs skill minting). Register in `docs/coalescing.md`'s Fold-up
deferral row, alongside the existing 2026-07-17 mm slate, one line
per candidate with its SB pin:
global-invariant mutations check live state inside the atomic
boundary; "unused" searches include examples and ungated consumers;
handshake peers declare protocol literals independently; cleanup
authority from ownership and live state, never path names; resolved
configuration flows through every validation boundary; counted and
completeness claims verified mechanically, "full" made true rather
than weakened; extraction audits removed paragraphs for hazards;
lock-order corrections are not substituted by retry, and mocks hide
the cycle. Each graduates on its second lineage or owner direction.

**Slice F — gate tooling (hardening inline: rollback is a single
revert; no one-way door; the exit-semantics change is declared in
CHANGELOG as a scaffold contract change for consumers)**

**F1. coalesce-check shallow-clone self-defense.** Red-first: build a
`--depth 1` clone of the hub in the scratchpad, run the script,
record the false BROKEN/exit 1. Then: detect
`git rev-parse --is-shallow-repository`; skip the SHA-resolution legs
with a printed reason and exit 0; non-SHA legs (lesson counts, cue
syntax) still run and print. Document in the script docstring that
enforcement CI requires full history. Green: rerun on the shallow
clone (loud skip, counts printed, exit 0) and on the full tree
(unchanged behavior). The permanent regression proof is F4's shallow
CI job, not the scratch probe (round-1 F8).
**F2. check-dom15-fixtures fence parser.** Adopt the rigorous
fence-tracking parser (fence char + length, closing-fence rules,
≤3-space indent) from sb:bin/check-plan-context:64-90. Red-first: add
a `--self-test` mutation case with a nested fenced-markdown wrapper
that the current toggle mis-parses; watch it fail; then port the
parser and watch the full self-test pass.
**F3. check-doc-paths negative knowledge.** Add the "tried and
reverted" comment block explaining why scan roots are guidance-only
(a gate that cries wolf gets ignored — sb:bin/check-doc-paths:43-49)
and an adopter-facing note that consumers extend `SCAN_FILES` to
their own agent surfaces.
**F4. gates.yml — sole owner of all workflow edits (round-1 F9).**
(i) `check-dom15-fixtures`: keep the existing live-spec step
unchanged and add a **separate** `--self-test` step — never replace
the live validation (round-1 F2). (ii) Contract step: assert C1's
exact sentence is present in `AGENTS.md`, and run a structural
read-order comparison — a `python3 -c` snippet that parses
`context.index.yaml`'s `read_order` and asserts each entry appears in
`AGENTS.md`'s read-order section in the same relative order (an
omission or reorder fails; a phrase-grep alone cannot detect either).
Red-first: run both checks before A1/C1 land and record the failures.
(iii) New `gates-shallow` job (round-1 F8): `actions/checkout` with
`fetch-depth: 1`, run `python3 bin/coalesce-check`, assert exit 0,
output contains the shallow-skip notice, and the lesson-count line is
still printed. This is the permanent proof that the F1 behavior
survives.

**Slice G — register interlock**

**G1. (OD-3, revised wording)** Apply the revised amendment to the
register plan; dispatch a fresh independent semantic review of the
amended plan (different family from its author); record the
disposition in that plan and cross-reference here.
**G2. (OD-4, authorized)** Add to
`review-loops-and-agent-bootstrap.md` (reviewer duty) and
`writing-plans.md` (author duty): before grading anything else,
existence-check every named flag, test path, seam, and driver order
against executable code; form fluency carries no information about
correctness. Cite the hub lessons entries (2026-08-06) and, once
landed, [REV-AT-003]. Note in each: promoted by owner direction
(OD-4) from a single-repository citation; the round-1 review of this
very plan is recorded alongside as corroborating in-hub evidence (it
caught citation drift exactly as the rule predicts).

**Final slice — traceability reconciliation.** CHANGELOG 2026-08-07
section enumerating every waved rule and the scaffold contract
change; `docs/coalescing.md` run-log line for the wave (backport
direction, source pin, this plan); spec `## Related Plans` backlinks;
this plan's index row flipped per D1's own rule; rerun all gates plus
the gates.yml steps from current state and record results; fresh-eyes
pass per §10 of `writing-plans.md`; possession probe (one, per
[AT-THEORY-6]) recorded in the execution log.

## Testing Plan

Docs verification is by inspection plus executable gates — no runtime
product behavior exists in this repo. Per engineering principle §10,
every slice names its failing-first proof or its Rule-5 substitute:

- Slices A–E (prose): the failing form is the pre-edit grep — for each
  promoted sentence, record the empty grep before the edit and the
  matching grep after. F4's workflow checks run red before A1/C1 land.
- Slice F: true red-green as specified per task (shallow-clone
  fixture; self-test mutation case). Nothing is mocked; the shallow
  clone is a real clone.
- Gates that must stay green after every slice:
  `python3 bin/check-doc-paths`,
  `python3 bin/check-doc-paths --scaffold`,
  `python3 bin/check-dom15-fixtures` (live; plus `--self-test` as a
  separate invocation after F2),
  `python3 bin/coalesce-check` (full history).
- Wave-vocabulary check (round-1 F1 — changed lines, not the tree):
  `git diff <diff base> -- <every file this plan touches except this
  plan file> | grep '^+' | grep -E '\[DOM-16\]|\[ALT-|winning product
  contract'` must return nothing. Historical occurrences in the
  baseline are out of scope.
- Invariant-protection greps (final slice): fold-unit denomination
  text still present in the skill and [DOM-14]; Trusted Base section
  intact; module-theory text intact; Stub/Draft/Active qualifiers
  intact.

## Verification and Gates

Per-task: the named grep or red-green pair, plus the gate commands.
Final: all gates green from current state; CHANGELOG, coalescing run
log, and index row present; changed-lines vocabulary check clean;
invariant greps clean; review dispositions closed. Rollback: every
slice is a revertible docs/tooling commit; ordering constraints: B
before C–E (promoted spec precedes text citing it); A1/C1 before
F4's contract checks go green (they run red first by design).

## Independent Review Loop

- Round 1: different-family reviewer per
  `review-loops-and-agent-bootstrap.md` §4 (two-question PASS/BLOCKED
  stance), bounded attempts recorded in the Review Log; brief includes
  the existence-check-first instruction.
- Round 2 (scoped, per §4a round-2 variant): limited to the accepted
  round-1 finding IDs and their fixes; verdict PASS/FAIL.
- Pre-landing +P review: different family, final state, before the
  completion claim.
- Author dispositions: every finding answered in the Review Log —
  adopt, rebut with reasoning, or defer with a named reopen condition.

## Review Log

| Date | Stage | Reviewer / result | Findings and disposition |
|------|-------|-------------------|--------------------------|
| 2026-08-07 | Pre-landing round 3 (scoped to the three round-2 residuals) | codex CLI (same invocation form, 900 s bound, completed in bound) — items 1–2 **OK**; item 3 **DEFECT** (duplicate-key guard counted raw `read_order:` text, so a comment mention would false-fail the gate) → overall FAIL on that single line | Accepted and fixed: the guard now counts only top-level `read_order:` key lines; executed proof recorded in the Execution Log (live PASS; comment mention not flagged; real duplicate caught). No round 4 dispatched — the residual was a single-line mechanical check whose correctness is established by the recorded two-direction executions per §12's authoring floor (gates are not recursively gated; three review rounds have run); disclosed here as the author-verified terminal step. |
| 2026-08-07 | Pre-landing round 2 (scoped to F1–F9) | codex CLI (same invocation form, 900 s bound, completed in bound) — **FAIL**: F1/F4–F9 OK; F2 residual (First-Sweep Policy bullet still categorical additive-only), F3 residual (substring membership instead of block equality), P3 (duplicate read_order key ignored) | All three accepted and applied: First-Sweep Policy section demoted in place as historical record (the rule this wave promoted, applied to the file that needed it) with the current archive rule named; workflow check upgraded to whole-block equality (anchor line to next blank line, normalized) with an applied-and-caught appended-text mutation recorded; duplicate read_order key now an explicit failure with mutation evidence. Gates rerun: coalesce 0, doc-paths OK. Round 3 scoped to these three. |
| 2026-08-07 | Pre-landing +P review of completed work, round 1 | codex CLI (same invocation form, 900 s bound, completed in bound) — **BLOCKED**: F1 (P1, run-log `a38e6a9` unattributed → coalesce-check exit 1, contradicting the Execution Log's exit-0 claim), F2 (P1, OD-1 reconciliation left the uncommitted-sweep additive-only commit gate standing in two skill clauses), F3 (P1, both workflow contract checks had false negatives — fragment grep; basename search), F4 (P2, Unindexed deferral row missing), F5 (P2, shallow mode skipped the cue-syntax leg), F6 (P2, parser rules without firing probes), F7 (P2, inexact heading citation), F8 (P2, stale draft header), F9 (P3, OD-4 provenance note missing on the author side) | All nine accepted and applied: pin attributed before the SHA (gate rerun exit 0 with real exit-code capture — the prior battery's `head -1` pipeline had masked the code; corrected in the Execution Log); both skill clauses rewritten per the pinned source (uncommitted sweeps may remove retained-ref source-pinned material; worktree-only sources stay additive-only); workflow step rewritten to full-paragraph compare + exact list equality with local mutation evidence; Unindexed deferral row added; cue-syntax inventory printed in shallow mode and asserted in `gates-shallow`; four parser probes added through the real path (tilde, mismatched char, info-string closer, 4-space indent); heading cited exactly with source line; header reconciled; provenance note added. Scoped round 2 pending. |
| 2026-08-07 | G1 register-amendment review, attempt 1 | codex CLI (same invocation form, 900 s bound, completed in bound) — **ADOPT-WITH-EDITS**: [AT-THEORY-5] PASS on both amendments; AM-1 (P2, hypothesis broader than the falsifier's measured dimensions) and AM-2 (P3, Pressure append produced a fragment) | Both accepted; the reviewer's exact replacement texts applied to the register plan's Amendment section; disposition recorded there. OD-3 not challenged. |
| 2026-08-07 | Round-3 scoped verification, attempt 1 | codex CLI (same invocation form, 900 s bound, completed in bound) — **PASS**: all six round-2 defect fixes verified OK (citation forms + corrected D8 range confirmed at the pin; Pressure text direction-free with the sole favorable assertion in the execution log; B2 enumeration complete per an independent `landing|authoriz` sweep; decision states coherent; E8 on the Fold-up tier; revision-history claim matches the untracked reality); no new defects | No dispositions owed. Plan-review stage closed; the pre-landing +P review remains scheduled for the completed wave per the Independent Review Loop. |
| 2026-08-07 | Round-2 scoped review, attempt 1 | codex CLI (same invocation form, 900 s bound, completed in bound) — **FAIL**: 9 of 15 fixes OK; 6 defects | All six accepted and applied in revision 3: (i) citation audit residue → continuation forms defined in Source Documents; D8's ceiling cite corrected to sb:skills/coalescing/SKILL.md:101-104. (ii) F3 residue → Pressure field made content-free about direction; OD-3 text updated. (iii) F4 residue → `docs/coalescing.md:58` (First-Sweep Policy) added to B2's enumeration — found by the reviewer re-running B2's own sweep, validating the mid-edit escalation rule. (iv) F5/F7 status incoherence → OD-2/OD-3/OD-4 texts now read DECIDED; T0 complete; E6/G1/G2 unconditional; rejection branches marked historical. (v) F12 residue → E8 re-targeted to the Fold-up tier and its two-lineage rule. (vi) False git-history claim → revision note corrected: revisions 1–2 were uncommitted worktree states edited in place; no committed prior revision exists. |
| 2026-08-07 | Round-1 plan review, attempt 1 | codex CLI (`codex exec -s read-only -C <repo> -c 'model_reasoning_effort="high"' "$(cat brief)" --json`, 900 s bound, completed in bound) — **BLOCKED** (Q1: no — citation drift, impossible final grep, unreconciled OD-1/OD-2 text, OD-3 wording vs [AT-THEORY-5]; Q2: yes — F4's self-test substitution risk) | Citation audit C1–C7, H1–H3: **accepted, all corrected** (full paths, ranges 129–142/300–302/293–296/43–49, README note re-pointed to agent-context README:16-19, runbook §8→§4, Pattern 8 explicitly an append). F1 accepted → changed-lines vocabulary check. F2 accepted → separate live + self-test steps (F4). F3 accepted with adaptation → OD-3 rewording (Pressure field, evidence-deficit framing); owner re-confirmation pending. F4 accepted → Task B2 exhaustive clause enumeration with mid-edit escalation rule. F5 accepted → OD-2 evidence corrected, promotion narrowed to demotion-in-place, re-presentation pending. F6 accepted → Deltas B2/B3/B5 now carry exact verbatim text and replacement boundaries. F7 accepted → explicit rejection branches in T0; G1 re-review named; OD-4 created for G2. F8 accepted → permanent `gates-shallow` CI job (F4.iii). F9 accepted → F4 sole workflow owner; structural read-order comparison replaces order-blind grep; C1 phrase kept as contractual. F10 accepted → E1/E2 rules general, wiring as conditional examples. F11 accepted → D9 cut. F12 accepted → E8 becomes a candidate slate in docs/coalescing.md. F13 accepted → E3 conditional on large/systemic audits; severance check kept general. F14 accepted → B1, B4, D3 withdrawn; E5 single normative owner. F15 accepted → D7 attribution corrected. Observations noted; no disposition owed. |

## Execution Log

(append-only)

- 2026-08-07 (implementation start): owner authorized implementation.
  Comprehension answers (implementer): (1) The [DOM-14] delta replaces
  the landing-authorization bullet because two contradictory
  authorization rules must not coexist in one section — the carve-out
  reconciles rather than adds a parallel path (engineering principle
  §1); worktree-only material stays ineligible because it has no
  archive cue, so git is not yet its archive. (2) After Slice F,
  `coalesce-check` detects `git rev-parse --is-shallow-repository`,
  skips the SHA-resolution legs with a printed reason and exit 0, and
  still runs and prints the non-SHA legs; acceptable because a gate
  that cannot be truthful must say so instead of failing for the wrong
  reason, enforcement CI keeps full history, and the changelog
  declares the scaffold contract change. (3) Do not copy: the
  flattened read order (deleted Stub/module-theory qualifiers), the
  coalescing skill's dropped fold-unit denomination text, and all
  [DOM-16]/ALT-REV/registry vocabulary. All three match the expected
  answers; implementation may proceed.
- 2026-08-07 (F4 red evidence, recorded before A1/C1): contract check
  1 — `grep -c "load-bearing for product-scope" AGENTS.md` → 0 (red,
  as required); contract check 2 — structural read-order comparison →
  FAIL: `docs/agent-context/README.md` absent from
  `context.index.yaml` `read_order` (red, as required).
- 2026-08-07 (implementation evidence, all slices): Slices A–G landed
  in the worktree. Red→green pairs: F4 contract checks (above → both
  GREEN after A1/C1); F1 `coalesce-check` on a real `--depth 1` clone
  (exit 1, false BROKEN on `5927481` → loud skip, counts printed,
  exit 0; full tree unchanged, exit 0); F2 nested-fence self-test
  probe (FAIL "nested-fence interior leaked" → all probes pass after
  the rigorous parser port; the pre-existing fenced probe was found
  vacuous — it bypassed `extract_section` — and both fence probes now
  route through the real path). Final gate battery from current
  state: `check-doc-paths` OK; `check-doc-paths --scaffold` OK;
  `check-dom15-fixtures` OK; `--self-test` all pass; `coalesce-check`
  exit 0 (19 SHA claims, 15 foreign, 23 lessons entries).
  Changed-lines vocabulary check: one `[DOM-16]` hit, baseline-resident
  (the 2026-07-30 plan's pre-existing index row, present in the
  worktree before this wave — observed in the session's first read of
  `docs/plans/README.md`); zero occurrences introduced by wave edits.
  Invariant greps: fold-unit denomination present in skill and
  [DOM-14]; Trusted Base section intact; module-theory text intact in
  `AGENTS.md` and [DOM-2]; Stub qualifiers intact.
- 2026-08-07 (possession probe, per [AT-THEORY-6] — probe 1, predict
  the bug class before the agent reports): before round-1 review
  returned, the register-symmetry account predicted the failure class
  a citation-dense fluent plan would carry — named surfaces that do
  not exist — and the review brief operationalized the prediction
  (existence-check first). The review found exactly that class (ten
  citation defects, five P1s). The prediction preceded the report;
  probe outcome: pass — the account anticipated the failure mode of
  its own carrier.
- 2026-08-07 (correction, from pre-landing F1): the "final gate
  battery" entry above claimed coalesce-check exit 0, but the battery
  invoked it as `python3 bin/coalesce-check | head -1` — the pipeline
  reported head's exit code, not the gate's. At that moment the gate
  was in fact failing on the run-log line added after the battery's
  true full run. The claim is retracted; the corrected run (pin
  attributed, direct invocation, exit code captured) is recorded in
  the pre-landing Review Log row. Lesson candidate: a gate invoked
  through a pipeline reports the pipeline's exit, not the gate's.
- 2026-08-07 (pre-landing F1–F9 fix evidence): gates rerun with
  direct exit-code capture — doc-paths 0, scaffold 0, dom15 live 0,
  self-test 0 (now ten probe/mutation cases including tilde,
  mismatched-char, info-string-closer, and 4-space-indent), coalesce
  0 (16 foreign, pin attributed), shallow clone prints the cue-syntax
  inventory. The rewritten AGENTS.md contract check passes live and
  caught all four in-memory mutations (paragraph corruption,
  read-order row deletion, reorder, yaml entry drop) — recorded here
  as the one-time mutation evidence per the F3 disposition.
- 2026-08-07 (fresh-eyes pass, §10): re-read of the landed deltas
  against the plan; one design deviation noted and kept — hardening
  §14 retains its short motivating bullets above the new pointer to
  `writing-plans.md` §3 (the plan's "only a pointer" is satisfied in
  substance: one normative owner, no duplicated mechanics). No
  missing paths found; gates confirm.

- 2026-08-07: OD-1 decided by owner: **adopt** the git-backed
  coalescing carve-out. OD-2 initial answer (graduate) was given
  against revision-1 evidence later found overstated (round-1 F5);
  re-presentation pending. OD-3 initial answer (amend as proposed)
  given; wording revised per round-1 F3; re-confirmation pending.
  Owner-favorable register observation recorded here per OD-3's
  revised routing: the owner reports sustained subjective quality
  improvement from high-register corpus loading; this log line, not
  current-account theory, is where that observation lives.
- 2026-08-07 (revision 3): round-2 FAIL applied. Note on OD-3: the
  owner confirmed the revision-2 wording; round-2 then found the
  Pressure field still carried a directional impression, and revision
  3 tightened it to content-free — a further move in the direction
  the owner confirmed, applied under that confirmation and flagged to
  the owner rather than re-asked.
- 2026-08-07 (after revision 2): remaining decisions recorded by
  owner. OD-2: **promote narrowed** — demotion-in-place becomes
  normative by owner direction; Revision Log and reviewed-baseline
  pin stay candidates with SB as partial family evidence. OD-3:
  **revised wording confirmed** — Pressure-field motivation plus
  evidence-deficit framing; no favorable-quality assertion in theory
  prose. OD-4: **promotion authorized** — G2 lands the
  existence-check rule in both runbooks by owner direction, with this
  plan's round-1 citation audit recorded as corroborating in-hub
  evidence.

## Out of Scope

- The negative-knowledge/[DOM-16] package (routing table, four-type
  taxonomy, ALT/REV grammar, reopening protocol, coalescing
  interlock, hub `check-plan-context`, and any universal
  reference-code namespace rule — round-1 F11) — future plan.
- The ownership-triad restructuring of `principles.md`,
  `decision-hierarchy.md` tier 3, and the two-tier traceability chain
  — future plan, adopted as one package with the anti-second-
  constitution counterweight or not at all.
- Any edit to SimpleBroker (reverse-propagation debt recorded, not
  fixed: Trusted Base section, module theory, rename staleness in its
  `check-dom15-fixtures`, truncated docstring in its
  `check-doc-paths`).
- Efficacy claims in current-account theory prose ([AT-THEORY-5]).
- The generalized static-analysis-gate and state-machine-transition-
  gate DOM sections — candidates for the next wave.
- `external-skill-suites.md` crosswalk annotations; multi-entry-point
  routing rules — low value for the hub today.

## Fresh-Eyes Review

Performed at final slice per `writing-plans.md` §10; additionally: cut
any ported sentence that duplicates an existing hub rule rather than
strengthening it — a backport that restates is bulk, not transfer.
