# Plan-Metadata Gate Plan

Date: 2026-08-11
Class: 4+P (effective 5) — a new executable gate plus material edits to
`docs/agent-context/runbooks/writing-plans.md` and the root `AGENTS.md`
Definition of Done: [DOM-6]-material to how future work is reviewed and
verified (+P). The gate is a new CLI-shaped tool (flags, parsed input,
public exit-code classes) — a [DOM-5] risky trigger, so class 4, with
the hardening checklist and review-before-implementation. No
`docs/specs/` normative text is edited (class-5 base does not fire).
Escalated 3+P → 4+P at review round 1 (codex finding F4); declared
here per the one-way escalator rule.
Status: draft — see index row
Review: 2026-08-11 codex rounds 1–4 — round 1 BLOCKED (5 findings),
round 2 scoped blocker F1–F4, round 3 FAIL (N1/N2), round 4 PASS; all
findings dispositioned in the Review Log. Awaiting owner ratification;
+P pre-landing review owed after implementation
Type: implementation with process-text revision; promotion strategy B
(atomic — guidance text, gate, and CI wiring land in one change; no
spec-tree link claims are involved)

## Revision Log

- **r1 (2026-08-11):** revised after codex round-1 BLOCKED verdict.
  Changes: class escalated to 4+P; plan-header `Status:` demoted to
  optional with a retirement-safe consistency rule (F1); cutover
  re-keyed to the filename date, header grammars tightened (F2);
  scaffold boundary decided hub-only-v1 with scaffold-safe wording
  (F3); acceptance-probe floor and hardening declarations added (F4);
  Deltas 3/4 reworded to claim exactly what they enforce (F5); fixture
  strategy switched to integrated-corpus + per-rule mutations while
  keeping a light rule registry (scope-cut, partial). Dispositions in
  the Review Log.

## Goal

Make obligation-state a checkable property of plan artifacts instead of
a property of lifecycle transitions the author may never cross.
Concretely: implement the structural status-index checker that the
plan-lifecycle section already prefers ("an executable checker for
missing, duplicate, dead-path, unknown-status, and malformed rows"),
extend it with a required `Review:` marker for new plans so an
unreviewed-and-silent draft becomes an impossible state, and add an
explicit authoring-runbook step anchoring **review-state declaration**
to the handoff — the one event every plan crosses. Motivating failure
(2026-08-11, consumer repo): a Class 5 plan was delivered as
`Status: draft` with no independent review; every mechanical gate
passed and no prose rule fired because every review obligation was
anchored to a downstream transition (promotion, completion) that a
draft handoff never crosses. This repository carries the same escape:
measured 2026-08-11, one plan file has no Status Index row, one active
plan's header contradicts its index row, and 5 of 15 plan files carry
the `Class:` line the runbook calls mandatory. Engineering principle
§12 predicts exactly this drift for prose-only conventions; the
corpus's prescribed remediation for a §12 violation is a firing gate,
not another prose rule (review-loops §5a).

## Source Documents

Source specs and normative surfaces:

- `docs/specs/01-development-documentation-operating-model.md`
  [DOM-15] (class table, declared-claim line, escalators), [DOM-11]
  (independent review), [DOM-14] (index/harvest mechanics), [DOM-5]
  (risky triggers — CLI shape)
- `docs/agent-context/runbooks/writing-plans.md` — Plan Lifecycle and
  Retirement (status vocabulary; "structured and gated" preference;
  the "binary status checker" sentence this plan clarifies; mutability
  boundary; soft-retirement mechanics), Required Plan Sections §8/§10
- `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md`
  §2–§6 (review policy — unchanged by this plan)
- `docs/agent-context/runbooks/hardening-plans.md` (class-4 checklist)
- `docs/agent-context/runbooks/adversarial-acceptance-probes.md`
  (CLI probe floors — mandatory for this tool)
- `docs/agent-context/engineering-principles.md` §12, §13
- `docs/agent-context/runbooks/writing-specs.md` gate-wiring rule
- `docs/lessons.md` 2026-08-06 entry (doctrine floors)
- Failure report and signature sweep, this session (2026-08-11)

Read-order declaration: program theory, agent-context README,
decision-hierarchy, principles, engineering-principles, writing-plans,
review-loops, hardening-plans (headers), lessons (Golden Rules +
post-watermark entries) were consulted this session.

## Context and Key Files

- `bin/check-dom15-fixtures` — the convention template: Python 3
  stdlib only, exit codes 0 clean / 1 violation / 2 invocation error,
  never prints a traceback, `--self-test` as a separate CI step,
  `strip_fenced_blocks` fence handling (reuse this logic — fence
  character + length tracking, adopted from simplebroker's
  `check-plan-context` at pin `a38e6a9`).
- `.github/workflows/gates.yml` — execution path; each checker runs
  live and `--self-test` as separate steps, never a replacement.
- `docs/plans/README.md` — the `## Status Index` section
  (`| Plan | Status |` rows) and the separate `## Retired Plans`
  ledger (different table; the checker must not conflate them).
- `docs/plans/*.md` — all 15 current filenames parse as
  `YYYY-MM-DD-<slug>.md`; headers vary (`Status:` free text, `Class:`
  in 5/15, `Date:` in newer plans only).
- `bin/bootstrap-agent-theory` — scaffolds consumers; does NOT copy
  the new checker (deliberate — see F3 disposition); the generated
  consumer index has its own vocabulary defects (spun off separately).
- `bin/check-doc-paths` — excludes `docs/plans/`; unchanged. Its
  `--scaffold` mode is why Delta 1 must use scaffold-safe phrasing.
- DOM-15's fixture-gate paragraph — the phrasing pattern to copy: the
  obligation stated generically, with "(this repository:
  `bin/check-dom15-fixtures`…)" naming the local wiring.

Comprehension questions (answers recorded in the Execution Log before
editing; a wrong answer blocks implementation):

- Q1: When the checker flags a row whose status is ambiguous or
  contradicts its plan header, what may the implementer NOT do, and
  what are the two legal moves? Expected: never rewrite status data to
  make the checker pass; repair to what the evidence supports, or
  quarantine the row as `status-review`.
- Q2: Why is the header/index consistency rule (PM-7) suspended when
  the index row says `retired-pending`? Expected: soft retirement
  flips only the index on a plan whose body is already immutable at
  closure; requiring the frozen header to track that flip would force
  editing an immutable record or failing CI (codex F1).
- Q3: Why is the cutover keyed to the filename date rather than the
  header `Date:` line? Expected: a cutover selected by the field whose
  absence it detects is self-disabling — a plan missing `Date:` would
  escape the very rule that requires `Date:` (codex F2). The filename
  is independently mandated, universally present, and parseable.

## Invariants and Constraints

- **Completion remains a declared claim.** The gate checks structure
  and consistency only; it never decides semantic done-ness.
- **Status data is never rewritten to make a checker pass** (existing
  lifecycle rule). Repairs cite evidence; ambiguity migrates to
  `status-review`.
- **Closed plans are immutable; the index is the sole lifecycle
  owner.** No backfill edits to completed/superseded plan bodies. The
  plan-header `Status:` is optional convenience, never authority, and
  its consistency rule (PM-7) is suspended at `retired-pending` so
  soft retirement never touches a closed body.
- **A schema cutover must not be selected solely by the field whose
  absence it is intended to detect** (new invariant, proposed by codex
  round 1 — adopted; raised for owner ratification with this plan).
- **Review policy is unchanged.** Who reviews, prompts, disposition
  loops stay owned by review-loops. This plan makes review *state*
  declarable and checkable; it does not force review before handoff.
- **Scaffold-safety:** guidance text landed by this plan must not
  create dangling path claims in scaffolded consumers. The
  `check-doc-paths --scaffold` scanner is **lexical** over backticked
  `docs/`/`skills/`/`bin/` tokens in copied files (codex round 2), so
  copied guidance (`writing-plans.md`, `AGENTS.md`) may not carry a
  backticked path to any non-copied tool — it says "the repository's
  configured structural checker (named in its CI gates)"; the exact
  hub command appears only in hub-only surfaces (this plan,
  `gates.yml`, `CHANGELOG.md`). The DOM-15 "(this repository: …)"
  pattern is safe only because `bin/check-dom15-fixtures` IS copied.
- **No new dependency** (Golden Rule 9): Python 3 stdlib only.
- **Gate-wiring rule**: the gate's execution path (gates.yml, live +
  self-test) is named in the same change that creates it.
- **Truthful exit codes**: 0 clean, 1 contract violation, 2 invocation
  error; no tracebacks; hostile input to one file must not abort the
  batch.
- **`bin/check-doc-paths` continues to exclude `docs/plans/`.**

## Hardening Declarations (class-4 checklist)

- Invariants: above, named before tasks.
- Hidden couplings: `docs/plans/README.md` has two tables (Status
  Index, Retired Plans ledger) — the checker binds only the Status
  Index section and must locate it by heading, not "first table".
  Bootstrap's generated consumer index is a second consumer of the
  index grammar — decided out of scope (F3), so no coupling lands.
- Anti-mocking: live CI invocation runs on the real tree; fixtures
  never substitute for it (separate steps).
- Rollback: revert one atomic change (gate + wiring + text); no
  runtime behavior, no persistence, no migration. Rollout sequencing:
  single landing; CI turns red only if the tree truly violates rules
  after the Task-4 repairs.
- One-way doors: none — watermark means no historical record is
  edited; the gate can be deleted cleanly.
- Post-deploy signal: gates.yml green on main after landing.
- Deferred/async lifecycles, persistence, cleanup: none introduced.

## Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## Spec Baseline

- `d52e12a` — `docs/agent-context/runbooks/writing-plans.md`,
  `AGENTS.md`, `.github/workflows/gates.yml`,
  `bin/bootstrap-agent-theory` at plan authoring time. Worktree note:
  four modified files unrelated to this plan (`docs/README.md`,
  `docs/agent-context/principles.md`,
  `docs/implementation/02-repository-map.md`,
  `skills/crystallize-program-theory/SKILL.md`) and untracked
  `docs/lore/` are in-flight owner work; this plan does not touch them.
- No `docs/specs/` file is edited. The delta targets are runbook and
  root-agent-file text (normative for process, hence +P).

## Proposed Guidance Delta

Exact text for review. Strategy B (atomic): these edits land together
with the gate and CI wiring in one change.

### Delta 1 — `writing-plans.md`, Plan Lifecycle bullet (replace)

Replace:

> **Class ≥3 completion is not claimed until the Status Index row exists
> and is `completed` or `superseded`.** Update `docs/plans/README.md` in
> the same change as the completion claim. Do not require a binary
> status checker; the index is the contract.

With:

> **Class ≥3 completion is not claimed until the Status Index row exists
> and is `completed` or `superseded`.** Update `docs/plans/README.md` in
> the same change as the completion claim. A repository adopting this
> lifecycle ships a structural checker over its plans directory and
> status index — missing, duplicate, dead-path, unknown-status, and
> malformed rows, plus the header block on plans dated at or after the
> repository's adoption watermark. The checker and its watermark are
> named in the repository's CI gates (agent-theory wires its
> plan-metadata checker there with watermark 2026-08-11). No checker
> decides semantic
> completion: whether the work is done remains a declared claim
> verified by evidence and review; the index is the contract for what
> is claimed, and the checker gates only its structure.

### Delta 2 — `writing-plans.md`, File Placement section (append)

> **Plan header block (plans whose filename date is on or after the
> repository's watermark; agent-theory's is 2026-08-11).** The header
> block is the contiguous run of nonblank lines starting at the first
> nonblank line after the H1 title and ending at the next blank line;
> the required fields below (`Date:`, `Class:`, `Review:`) appear
> exactly once there, optional `Status:` at most once, and text
> outside the block never satisfies a header rule. Checked
> structurally by the repository's configured checker (named in its
> CI gates):
>
> - `Date: YYYY-MM-DD` — must equal the filename date
> - `Class: <N or N+P>` (N in 0–5) followed by one-line trigger
>   reasoning ([DOM-15])
> - `Review: pending` **or** `Review:` followed by at least one
>   recorded round. The checker proves only the shape — an ISO date
>   plus non-empty text; that the text names the reviewer family and
>   verdict, with the full record in the plan's review log, is
>   review-verified content
> - `Status: <token> — <free text>` is **optional** (the index owns
>   lifecycle state); when present, `<token>` must be an index
>   vocabulary token and match the plan's index row — except when the
>   index row says `retired-pending`, which flips after the plan body
>   is closed and immutable
>
> `Review: pending` is legal — drafts are real. An absent `Review:`
> line is the violation: unreviewed-and-silent is not a representable
> state. A plan whose index status is `completed` or `superseded` must
> not carry `Review: pending`.

### Delta 3 — `writing-plans.md`, after §10 Fresh-Eyes (new final step)

> ### 11. Declare Review State Before the Plan Leaves the Session
>
> Review-state **declaration** anchors to the handoff — the one event
> every plan crosses — not to "complete", "promotion", or any other
> vocabulary the author may never utter. Independent review itself may
> legitimately still be pending at handoff; hiding that state is the
> defect. Before a class ≥3 plan is handed off — pasted, committed, or
> left as the session's deliverable:
>
> 1. run the independent review (review-loops §4) and record the
>    round in the plan, **or** set `Review: pending`;
> 2. run the repository's configured structural checker (named in its
>    CI gates) and confirm the header block and Status Index row
>    exist and agree;
> 3. state the review state in the handoff message explicitly —
>    "reviewed by X (verdict)" or "review pending".
>
> The handoff-message declaration (step 3) is universal — it applies
> to every class ≥3 plan regardless of age. The in-plan `Review:`
> marker (steps 1–2) applies to plans dated on or after the
> repository's watermark; never edit a closed pre-watermark plan body
> to add markers — declare its review state in the handoff message
> and, while it is live, in its index row.
>
> The escape this step closes: an unreviewed plan handed off as a
> deliverable while never crossing any transition a review rule was
> anchored to (observed 2026-08-11 in a consumer repository).

### Delta 4 — `AGENTS.md` (two edits)

In Project Conventions, after the "Non-trivial plans should receive…"
bullet:

> - Any plan handed off in any state declares its review state — a
>   recorded round or an explicit "review pending" — in the handoff
>   message, and additionally in the plan header (`Review:` line) for
>   plans dated on or after the repository's watermark (see
>   `writing-plans.md` §11). A handoff silent about review state is a
>   defect even when no completion is claimed.

In the Definition of Done, after the "an independent review has been
run…" bullet:

> - every plan handed off during the work satisfied the review-state
>   declaration rule (`writing-plans.md` §11)

### Delta 5 — `docs/lessons.md` (dated entry, 2026-08-11)

> - **An obligation anchored only to a self-declared transition is
>   defeated by never uttering the claim.** A Class 5 plan was handed
>   off as `Status: draft`, unreviewed; every review obligation was
>   keyed to "complete"/"promotion"/"integration-ready", so no rule
>   fired while the intent was fully violated. The artifact carried no
>   marker distinguishing a reviewed draft from an unreviewed one, and
>   the mechanical gates' green produced a false done-signal. Fix
>   pattern: anchor enforcement to events every artifact crosses
>   (authoring, handoff), and give every obligation an artifact-level
>   marker where silence is illegal — declare-or-do, the same shape as
>   `hardening: N/A — no risky trigger` and "report the uncommitted
>   state instead of calling the work done". The marker half was
>   already law (2026-08-06: floors are "gate, or declared claim plus
>   review — never neither"); the transition half is this entry. A
>   checker corollary from the same incident's remediation review: a
>   schema cutover must not be selected solely by the field whose
>   absence it is intended to detect. Applied:
>   `bin/check-plan-metadata` + writing-plans header block + §11
>   handoff declaration (plan 2026-08-11). Golden Rule candidate —
>   owner decision.

### Delta 6 — `CHANGELOG.md` (entry)

> ## 2026-08-11 (plan-metadata gate; review state becomes checkable)
>
> - `bin/check-plan-metadata` + `gates.yml`: structural gate over
>   `docs/plans/` — index row shape/consistency for all plans, header
>   block (`Date`/`Class`/`Review`, optional retirement-safe `Status`)
>   for plans with filename date ≥ 2026-08-11. `Review: pending` is
>   legal; absent is not.
> - `writing-plans.md`: "binary status checker" sentence clarified
>   (structural gating preferred and now wired; semantic completion
>   stays a declared claim); new §11 anchors review-state declaration
>   to the handoff. `AGENTS.md`: handoffs declare review state;
>   Definition of Done references §11. Motivated by a consumer-repo
>   escape (unreviewed Class 5 draft handed off; no
>   transition-anchored rule fired).

## Tasks

**Stop-and-re-evaluate gate (applies to every task):** if
implementation requires weakening any PM rule, changing the exit-code
classes, adding a dependency, or crossing the hub-only scaffold
boundary (copying the checker or naming its path in copied guidance),
stop and re-enter review before continuing — do not adapt silently.

1. **Write `bin/check-plan-metadata`.**
   - Files: `bin/check-plan-metadata` (new, executable).
   - Read first: `bin/check-dom15-fixtures` (docstring shape,
     exit-code contract, `strip_fenced_blocks`, argument pattern
     `[--plans-dir PATH] [--index PATH] [--self-test]`).
   - Architecture: a small ordered registry of rule functions (id,
     description, callable) over a parsed model (plan files with
     header fields; index rows from the `## Status Index` section
     located by heading). Adding a rule appends a function and its
     mutation fixture. No plugin machinery beyond the list.
   - Rules (watermark = filename date ≥ 2026-08-11):
     - **PM-0** every `docs/plans/*.md` except `README.md` has a
       filename parsing as `YYYY-MM-DD-<slug>.md` with a valid
       calendar date. All plans.
     - **PM-1** every plan file has exactly one Status Index row
       (missing / duplicate). All plans.
     - **PM-2** every Status Index row names an existing plan file
       (dead-path). All rows.
     - **PM-3** every row is well-formed (`| <file> | <status text> |`)
       and its leading status token is in the closed vocabulary
       (`draft`, `active`, `status-review`, `completed`, `superseded`,
       `retired-pending`). `exemplar` is free-text marker inside a
       `completed` row, not a token. All rows. The Retired Plans
       ledger table is out of the checker's scope.
     - **PM-4** (watermarked) the header block — the contiguous run
       of nonblank lines starting at the first nonblank line after
       the H1 title and ending at the next blank line — contains,
       each exactly once, `Date:` equal to the filename date and
       `Class:` matching `[0-5](\+P)?` followed by non-empty
       reasoning and a `Review:` line. Duplicated required fields are
       a violation; matching lines outside the block never satisfy a
       rule.
     - **PM-5** (watermarked) `Review:` value is exactly `pending` or
       contains an ISO date (`\d{4}-\d{2}-\d{2}`) plus non-empty
       further text. The checker proves shape only; reviewer family
       and verdict are review-verified content (Delta 2 states this
       division explicitly).
     - **PM-6** (watermarked) index status `completed`/`superseded` ⇒
       `Review:` is not `pending`.
     - **PM-7** (watermarked) `Status:` header is optional, at most
       once in the block; when present, its leading token is in the
       vocabulary and equals the index-row token, **unless** the
       index row is `retired-pending`. A duplicated `Status:` line is
       a violation.
     - Pre-watermark plans: PM-0/PM-1 only on the file side; their
       headers are never read (immutability; legacy vocabulary like
       `Promoted` stays untouched).
   - Robustness floors (also probed in Task 5): unreadable or
     non-UTF-8 plan file → per-file violation, batch continues;
     missing plans directory or missing/heading-less index → exit 2
     invocation error with a printed reason; unknown flags → exit 2;
     no code path prints a traceback.
   - Done signal: `python3 bin/check-plan-metadata --self-test`
     exits 0.
2. **Wire into `gates.yml`**: two steps (live, `--self-test`)
   following the existing per-checker convention. Done: step list
   mirrors other checkers.
3. **Apply Deltas 1–5** exactly as written (or as revised by round 2).
   Done: diff matches delta text; `check-doc-paths --scaffold` stays
   green (scaffold-safe phrasing verified, not assumed).
4. **Repair live defects (evidence-first, never checker-first):**
   - Add the missing Status Index row for
     `2026-08-07-commit-subject-principle-promotion-plan.md`:
     `| 2026-08-07-commit-subject-principle-promotion-plan.md | draft — promotion candidate; unindexed 2026-08-07..2026-08-11, row added by plan 2026-08-11 |`.
   - `2026-07-14-call-agent-skill-plan.md` header (`Draft — awaiting
     pre-landing review`) vs index (`active — promoted after +P
     review`): verify from the plan's own review log and git history;
     repair the false side to the evidenced state, or flip the index
     row to `status-review` if evidence cannot distinguish. Record
     evidence in the Execution Log. (Pre-watermark, so PM-7 will not
     check it — the repair is owed to truth, not to the checker.)
   - Done: `python3 bin/check-plan-metadata` exits 0 on the real tree.
5. **Acceptance probes** (adversarial-acceptance-probes floors — the
   gate is a CLI): run and record black-box probes from outside the
   implementation: hostile/non-UTF-8 plan file (batch continues, exit
   1, no traceback); grammar mimicry inside fenced blocks (inert);
   malformed and duplicate index rows; index file with the Status
   Index heading absent vs index file absent vs plans dir absent
   (exit 2, printed reason, no traceback); unknown flag (exit 2);
   empty plans dir (exit 0 vacuous or explicit — decide and document);
   default run from repo root self-applies to the real tree. Done:
   each probe's command + observed exit code + output line recorded
   in the Execution Log.
6. **Add Delta 6 (CHANGELOG).**
7. **Final gates**: run every gates.yml command locally from current
   state; record outputs in the Execution Log.

## Testing Plan

- Harness: `--self-test` inside the checker (this repo has no
  `tests/` directory; bin self-tests + CI are the declared execution
  path), plus the Task-5 black-box probes run from outside the
  implementation.
- Fixture strategy (per codex round-1 scope cut, accepted): one
  integrated valid corpus fixture (plans + index as inline strings),
  then one mutation per rule id flipping exactly that rule to firing,
  plus targeted interaction cases (retired-pending with frozen
  `Status:` header passes PM-7; pre-watermark plan with `Promoted`
  header passes; watermarked plan absent `Review:` fails PM-4) and
  exit-code fixtures (0/1/2). Every PM rule and exit code has a firing
  fixture — a gate shipped without firing fixtures is the defect it
  exists to catch (engineering principle §12, reflexively).
- Anti-mocking: the live invocation runs against the real
  `docs/plans/` tree and real index; fixtures prove rule logic, the
  live run proves the tree; both are separate CI steps. Nothing is
  mocked.
- Docs edits verified by inspection: quote changed guidance lines in
  the completion report.

## Verification and Gates

Per-task: as listed above. Final gates before any completion claim:

```
python3 bin/check-plan-metadata --self-test
python3 bin/check-plan-metadata
python3 bin/check-dom15-fixtures && python3 bin/check-dom15-fixtures --self-test
python3 bin/check-doc-paths && python3 bin/check-doc-paths --scaffold
python3 bin/coalesce-check
```

plus the AGENTS.md-contracts inline check from gates.yml. Success: all
exit 0; the live plan-metadata run passes only because the tree is
actually repaired (Task 4), not because rules were weakened.

Rollout/rollback: no runtime behavior; revert one atomic change.
One-way doors: none.

## Independent Review Loop

- Reviewer: **codex** (different family; review-eligible per
  `docs/implementation/03-agent-inventory.md`), via
  `codex exec -s read-only -C "$(git rev-parse --show-toplevel)"
  "$PROMPT" --json < /dev/null` with
  `-c 'model_reasoning_effort="high"'` (skills/call-agent). Bounded
  attempts: two per round, 10-minute timeout, recorded in the Review
  Log; fallback per review-loops §2.
- Round 1 (plan review, §4 prompt): completed — BLOCKED; dispositions
  below. Round 2 (scoped change review, §4a prompt over the r1 delta):
  required before implementation begins (class-4 gate).
- +P pre-landing review: a further codex round over the actual diff
  before the work is offered for landing.
- Owner gate: durable-guidance promotion — agent review supports but
  does not substitute for owner ratification ([DOM-15] Rules). The
  adopted cutover invariant (Invariants, above) is explicitly flagged
  for owner ratification. Nothing lands without it.

## Out of Scope

- The other transition-anchored escape sites found 2026-08-11 — probe
  manifests for the existing `bin/` CLIs, existence-check markers, a
  verified-against column in spec deltas, `bin/coalesce-check`
  computing the plans-tier counts the session-start check names.
  Reopens when: this gate lands and the owner schedules the follow-up
  sweep.
- Scaffolding `bin/check-plan-metadata` into consumers, and the
  bootstrap generated-index defects codex found (vocabulary omits
  `status-review`, wrongly lists `retired`; legacy-boundary semantics)
  — spun off as a separate task; Delta 1/2 phrasing is scaffold-safe
  either way. Reopens when: propagation runs after hub landing, or
  the spun-off bootstrap fix is picked up.
- Any `docs/specs/` edit, including extending [DOM-15]'s
  handoff-report concept to classes 3+ in spec text. Reopens when:
  owner wants the doctrine in the operating model itself (class-5
  base, separate plan).
- Golden Rule promotion of the Delta 5 lesson (owner decision).
- Backfilling headers into pre-watermark plans (immutability).

## Review Log

(append-only)

- **2026-08-11 — round 1, codex (plan review, §4 prompt, attempt 1,
  ~4 min): BLOCKED.** Findings and dispositions:
  - **F1** Plan-header `Status:` mirror breaks soft retirement
    (immutable closed body vs index flip to `retired-pending`).
    **Accepted, refined**: `Status:` header demoted to optional;
    PM-7 checks consistency only when present and suspends at
    `retired-pending`. Full removal (codex's suggestion) was not
    taken: the observed call-agent drift is header-vs-index on a
    *live* plan, exactly what a presence-conditional check catches;
    rationale recorded here per the deviation rule.
  - **F2** Self-referential cutover (`Date:`-keyed rule detecting
    missing `Date:`); grammars too loose. **Accepted**: cutover
    re-keyed to filename date (PM-0 makes the key universal);
    `Class:`/`Review:` grammars tightened; codex's proposed invariant
    adopted verbatim and flagged for owner ratification. Residual
    risk, declared: deliberate filename backdating defeats the
    watermark — that is a good-faith boundary; structural gates here
    do not defend against dishonest authors (the declared-claim floor
    and review do).
  - **F3** Scaffold boundary missing: runbook is copied to consumers,
    checker is not; `check-doc-paths --scaffold` would fail Delta 1
    as originally worded. **Accepted, decided hub-only-v1**: Deltas
    1–3 use the DOM-15 fixture-gate phrasing pattern (generic
    obligation + "this repository: …" wiring), making consumers'
    copies name their own obligation without a dangling path;
    scaffolding the checker itself and the bootstrap index defects
    are spun off (Out of Scope). Raised to owner as directed.
  - **F4** Under-classified; CLI probe floors missing. **Accepted**:
    escalated 3+P → 4+P (declared in header per the one-way escalator
    rule); hardening declarations added; Task 5 probe floor added;
    review-before-implementation now binds (round 2).
  - **F5** Delta 3 claimed to anchor review but anchors declaration;
    Delta 4 was self-contradictory ("completion-gate failure with no
    completion claimed"). **Accepted**: Delta 3 retitled and reworded
    to claim exactly the declaration; Delta 4 split into a Project
    Conventions handoff rule plus a Definition-of-Done reference to
    it.
  - **Scope cut** (drop rule registry + per-rule fixture pairs).
    **Partially accepted**: fixture strategy switched to
    integrated-corpus + per-rule mutations (codex's shape); a minimal
    ordered rule-function registry is retained — extensibility is an
    explicit owner requirement for this gate, and a flat list of
    functions is the same complexity class as `check-dom15-fixtures`'s
    internal structure.

- **2026-08-11 — round 2, codex (scoped change review, §4a prompt,
  attempt 1, ~5 min): `blocker: F1, F2, F3, F4`** (round-2 IDs, not
  round-1's). Confirmed resolved from round 1: PM-7 (retirement
  lifecycle, including later soft retirement) and PM-0 (cutover
  self-reference). Findings and dispositions:
  - **F1 (P1)** "this repository: …" phrasing is NOT scaffold-safe:
    `check-doc-paths --scaffold` is lexical over backticked `bin/`
    tokens in copied files, and the new checker is deliberately not
    copied; the DOM-15 pattern works only because that checker is
    copied. **Accepted**: copied guidance now says "the repository's
    configured structural checker (named in its CI gates)"; exact hub
    command confined to hub-only surfaces. Scaffold-safety invariant
    rewritten with the verified scanner behavior.
  - **F2 (P2)** header-block boundary and duplicate-field behavior
    undefined; PM-5's "two further words" proves less than Delta 2
    claimed. **Accepted**: block defined (title to first blank line;
    fields exactly once; outside text inert); PM-5 kept structural and
    Delta 2's prose narrowed to exactly what the checker proves.
  - **F3 (P1)** Deltas 3/4 quantified over pre-watermark plans the
    checker never reads, and "any state" could force editing closed
    legacy bodies. **Accepted**: handoff-message declaration stays
    universal; the in-plan marker is watermarked; editing closed
    pre-watermark bodies to add markers is explicitly forbidden.
  - **F4 (P2)** class-4 plan lacked a stop-and-re-evaluate gate
    ([DOM-5] review-readiness floor). **Accepted**: shared stop gate
    added atop Tasks (weakening a PM rule, changing exit classes,
    adding a dependency, or crossing the scaffold boundary → stop and
    re-enter review).

- **2026-08-11 — round 3, codex (round-2 verification variant,
  attempt 1, ~4 min): FAIL** — F1, F3, F4 verified PASS; the F2 fix
  introduced two new defects:
  - **N1 (blocking)** the block definition ("between the H1 and the
    first blank line") made this plan's own header fall outside the
    block (blank line at line 2). **Accepted**: block redefined as the
    contiguous nonblank run starting at the first nonblank line after
    the H1, ending at the next blank line (Delta 2 and PM-4).
  - **N2 (blocking)** `Status:` was simultaneously "exactly once" and
    "optional". **Accepted**: required fields exactly once; optional
    `Status:` at most once when present (Delta 2, PM-4, PM-7).
- **2026-08-11 — round 4, codex (round-2 verification variant over
  N1/N2 only, attempt 1, ~3 min): PASS.** N1 and N2 verified in all
  three locations; self-application confirmed (this plan's header
  block is its lines 3–19 under the amended rule; one of each field;
  `Date:` matches filename; `Status: draft` matches the index row).
  No new defects. Plan-phase review loop closed: every round-1 and
  round-2 finding accepted-and-addressed or dispositioned with
  recorded reasoning; nothing rejected silently. Remaining before
  implementation: **owner ratification** (durable-guidance promotion,
  [DOM-15] Rules), including the adopted cutover invariant and the
  hub-only-v1 scaffold boundary. The +P pre-landing review (over the
  actual diff) remains owed after implementation.

## Execution Log

(comprehension answers and evidence land here before editing)
