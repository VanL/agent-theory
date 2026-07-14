# Task Class Matrix Plan

Status: Promoted 2026-07-14 — four codex rounds plus one outside review
dispositioned (§8a–§8e). Round 4 verified seven of eight fixes correct
and blocked on one single-sentence invariant contradiction (§8e), fixed
and verified by inspection; a fifth round to re-check one sentence was
declined under the amended [DOM-11] performative-overengineering lens.
Own classification: Class 5+P; hardening: N/A — no [DOM-5] risky trigger
fires (process-material, no async/contract/storage/CLI edge)
Plan type: spec-authoring (the spec text is the primary deliverable; no
code cites it)
Promotion strategy: D — spec-authoring/clarification; all deltas land
atomically after review, no link claims involved

## 1. Goal

Add task classification to the operating model: classes that hold the
falsifiable verification floor constant everywhere while scaling planning
artifacts and review machinery with blast radius. Resolves the
three-reviewer tension (two demanded less ceremony, one demanded more)
with the principle: pedantry about verification always; paperwork
proportional to irreversibility. Uniform oversized ceremony decays into
performative compliance, which is high-variance; a right-sized mandatory
floor gets genuine compliance.

## 2. Source Documents

Source specs:
- `docs/specs/01-development-documentation-operating-model.md`
  [DOM-5] (owns the non-trivial and risky trigger lists — cited, never
  restated), [DOM-6] (materiality — the class-5 and class-P trigger),
  [DOM-10] (verification floor), [DOM-11] (review), [DOM-14] (classes
  1–2 reduce future plan-harvest load)
- `docs/agent-context/engineering-principles.md` §10 and
  `docs/agent-context/runbooks/testing-patterns.md` Rule 5 — Delta 6
  resolves their latent conflict, which [DOM-15]'s floor definition
  depends on

Review evidence: review passes 1–2 (coalescing plan §8a), codex pass 1
(external-skill-suites plan §7a findings 7/8/10), codex pass 2 on this
plan (§8a below), `docs/lessons.md` 2026-07-14 entry.

## 3. Context and Key Files

- `docs/specs/01-development-documentation-operating-model.md` — new
  [DOM-15]; two-sentence [DOM-5] routing amendment.
- `docs/agent-context/engineering-principles.md` — §10 amendment
  (Delta 6) resolving the substitute-proof conflict explicitly.
- `docs/agent-context/decision-hierarchy.md`,
  `docs/agent-context/runbooks/writing-plans.md`, `AGENTS.md` — pointer
  edits only (Deltas 3–5).
- `docs/plans/README.md` — status index.
- Scaffold: all edited files already in COPIED_FILES; no script edit
  expected; verified by dry-run.

Read first: [DOM-5]'s two trigger lists; [DOM-6]'s materiality sentence;
decision-hierarchy's preflight; codex round-1 findings in §8a.

## 4. Invariants and Constraints

- **The falsifiable floor never scales.** No class exempts: evidence
  lines; completion claims backed by reruns; firing tests for touched
  enumerable contracts; failing-test-first with §10-as-amended's named
  exit (never silent); declared deviations; formatter ownership; no AI
  attribution; dirty-tree discipline. If a class row appears to relax
  any of these, the row is wrong.
- **One canonical owner, by reference only.** [DOM-15] triggers are
  defined as "any [DOM-5] non-trivial trigger", "any [DOM-5] risky
  trigger", and "[DOM-6] requires" — never paraphrased subsets.
- **Classification depends on what the change requires, not what the
  author chooses to produce.** Class 5 fires when [DOM-6] *requires* a
  spec change or normative spec text is edited — omitting the required
  spec update is a violation, not a downgrade.
- **Floors accumulate; planning artifacts subsume; hardening is
  trigger-gated.** Review and verification floors accumulate up the
  classes; a higher-class plan replaces lower-class planning records
  rather than adding to them; the hardening-plans checklist is required
  by the class-4 trigger, never by inheritance — [DOM-5] risk and
  [DOM-6] materiality are different axes and combine only when both
  fire.
- **The unit of work is the whole requested outcome.** Slices inherit
  the unit's minimum class; decomposition never launders a class-3
  outcome into class-1 pieces.
- **Classification is a declared claim,** made before the first edit, in
  the session, and recorded in the class's work product (plan file for
  3+; commit/PR description for 1–2, or the handoff report when work is
  intentionally left uncommitted). Escalators are one-way and declared.
- Existing plans remain valid; the matrix applies from promotion forward.

## 4a. Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## 4b. Spec Baseline

- `01eb0b5` — docs/specs/01-development-documentation-operating-model.md
  and docs/agent-context/engineering-principles.md at plan authoring
  time (clean tree).
- Promotion baseline identifier: `39cea02` — Deltas 1–8 applied to the
  spec tree and all §6 gates rerun green at that commit (checker
  self-test and live run, exact grep list, backstitch 15/0/0/0,
  scaffold path assertions).

## 4c. Proposed Spec Delta

Promotion strategy: D. All deltas land in one change after review.

### Delta 1 — new section in `docs/specs/01-development-documentation-operating-model.md`, inserted after [DOM-14], before `## Related Plans`

> ## 15. Task Classification [DOM-15]
>
> Every unit of work is classified before the repository preflight or
> first edit. The unit of work is the whole requested outcome; slices
> inherit the unit's minimum class. Classification scales planning
> artifacts and review machinery; it never scales the verification
> floor — evidence lines, completion claims backed by reruns from
> current state, firing tests for touched enumerable contracts,
> failing-test-first with its named exit (engineering principle §10),
> declared deviations, formatter ownership, no agent self-attribution,
> and dirty-tree discipline apply identically at every class.
>
> The class is the **highest trigger that fires**, judged by what the
> change requires — not by what the author chooses to produce:
>
> | Class | Fires when | Planning artifact | Review |
> |-------|-----------|-------------------|--------|
> | 0 — Read-only | Nothing in the repository changes | None | None; claims cite evidence and distinguish verified from inferred |
> | 1 — Trivial | A change with no observable behavior change and no normative doc force (typos, comments, link repairs, formatting) | Classification line plus what/why/verification, recorded in the commit message — or in the handoff report when the work is left uncommitted for review | None |
> | 2 — Small | Observable behavior changes but **conforms to existing intended behavior**, evidenced by something independently inspectable — a governing spec section, an explicit user requirement in the session, or an existing contract test. Author inference is not intent evidence; without it, the class is 3. Also requires: reversible, and **no [DOM-5] non-trivial or risky trigger fires** | The abbreviated preflight, pre-edit: (1) outcome checklist, (2) the intent evidence or `Source spec: None — <reason>`, (3) invariants that must not move, (4) the planned verification command. The observed result is appended at completion. Recorded in the commit/PR description or handoff report | Author fresh-eyes |
> | 3 — Standard | Any **[DOM-5] non-trivial trigger** | Full dated plan per `runbooks/writing-plans.md`, status-index row, deviation log | Independent review of the plan **and** of the completed work ([DOM-11]) |
> | 4 — Risky | Any **[DOM-5] risky trigger** | Class 3 plus the hardening-plans checklist | Class 3 plus review before implementation begins |
> | 5 — Spec-changing | **[DOM-6] requires a spec change** (whether or not one has been drafted), or any normative spec text is edited — including clarification-only edits, which use promotion strategy D per `writing-plans.md` §4c | Class 3 plus spec baseline, exact proposed delta, named promotion strategy; the hardening-plans checklist **only if a [DOM-5] risky trigger also fires** — otherwise declare `hardening: N/A — no risky trigger` | Class 3 reviews plus independent review of the delta before the spec-promotion slice; review-before-implementation when hardening applies |
> | +P — Process-changing (modifier, not a class) | The change is [DOM-6]-material to how future work is **planned, implemented, reviewed, or verified** — regardless of which surface hosts it. A non-material edit to a skill or runbook (a typo, a link fix) is not +P; a material process change hiding in an "implementation" doc is | Declared as `Class N+P`; effective requirements are `max(N, 5)`'s | Effective class's review plus pre-landing review, different agent family preferred |
>
> Rules:
>
> - the review and verification floors accumulate; planning artifacts
>   **subsume**: a higher-class plan replaces the lower-class records, it
>   does not add to them (a class-3 plan is the planning record — no
>   separate class-2 preflight note is owed). The hardening-plans
>   checklist is required by the class-4 trigger, never by inheritance:
>   class-5 work with no [DOM-5] risky trigger declares `hardening: N/A —
>   no risky trigger` instead of writing empty rollback sections. [DOM-5]
>   risk and [DOM-6] materiality are different axes; they combine when
>   both fire
> - class-3 independent review may return a short structured brief —
>   goal, class claim, invariants, verification, top risks. The brief is
>   an **output** form only: the reviewer still receives the canonical
>   inputs (governing spec, plan, touched files) and the disposition loop
>   still runs in full. Classes 4 and 5 keep the full output bar. Author
>   fresh-eyes substitutes for independent review only when no second
>   agent is available, with the limitation disclosed — at every class
> - classification is a one-line declared claim citing its trigger
>   reasoning ("Class 2: restores [XYZ-3] intent, reversible, no DOM-5
>   trigger"); an undeclared class on non-read-only work fails the
>   completion gate
> - escalators are one-way and declared mid-flight: when any [DOM-5]
>   trigger or [DOM-6]-material discovery fires during work, the class
>   rises to that trigger's class at that moment. The engineering
>   warning signs (a second path appearing, rollback becoming
>   undescribable) are not triggers of their own — they force
>   re-classification against the same [DOM-5]/[DOM-6] lists. Silent
>   continuation at the old class is the violation, not the escalation
> - `+P` is a modifier: it combines with the base class as
>   `max(base, 5)` plus the pre-landing different-family review; there
>   is exactly one declaration format, `Class N+P`
> - classes 1–2 keep their record in the commit history (or the handoff
>   report when uncommitted) — git is the ledger for small work, which
>   also keeps `docs/plans/` free of [DOM-14] harvest debt
> - when classification is genuinely uncertain after reading the [DOM-5]
>   lists, ask once, narrowly
>
> Classification fixtures. This table is [DOM-15]'s enumerable contract
> (engineering principle §12) and carries an executable gate: a
> repository adopting this section ships a structural checker that fails
> when a fixture names an unknown class, a class or the `+P` modifier
> has no fixture, a class-1/2 fixture omits its negative-trigger facts,
> or the cumulative-requirements rule is absent (this repository:
> `bin/check-dom15-fixtures`, exit nonzero on violation). Semantic
> classification of real tasks remains judgment, verified by the
> declared-claim line and by review; repositories with test harnesses
> additionally encode these fixtures as firing tests over their own
> tooling. Fixture rows state their trigger facts explicitly — class
> follows from the stated facts, never from file topology. Edits to
> [DOM-5]'s trigger lists update these fixtures in the same change: the
> checker enforces presence, review enforces meaning.
>
> | Fixture (trigger facts stated) | Class |
> |---------|-------|
> | Answer an architecture question; survey a repo — nothing changes | 0 |
> | Fix a spelling error; repair a broken doc link — no behavior change, no normative force, no [DOM-5] trigger fires | 1 |
> | Behavior-preserving refactor, one module, following the established pattern — given: no [DOM-5] non-trivial or risky trigger fires (in particular, no zero-context ambiguity) | 1 |
> | Behavior-preserving refactor across two modules with unclear ownership — zero-context ambiguity, a [DOM-5] non-trivial trigger, fires | 3 |
> | Bug fix restoring validation that spec section `[XYZ-3]` requires — the cited section is the intent evidence; reversible; given: no [DOM-5] trigger fires | 2 |
> | Same fix, but no spec, no stated user requirement, no contract test — intent evidence absent | 3 |
> | Fix spanning a producer and a consumer — given: the two sides are distinct major surfaces, so a [DOM-5] non-trivial trigger fires | 3 |
> | Same shape, but both sides live inside one module — reversible, spec-cited intent, and no other [DOM-5] trigger fires | 2 |
> | Implement an already-specified CLI flag — CLI shape changes ([DOM-5] risky) | 4 |
> | Introduce background or deferred processing whose intended behavior an existing spec already governs — a [DOM-5] risky trigger fires; no [DOM-6] spec change is required | 4 |
> | Clarify normative spec wording, behavior unchanged — normative spec text edited; no risky trigger, so `hardening: N/A` | 5 (strategy D) |
> | New feature whose intended behavior is undocumented and [DOM-6]-material — a spec is required first | 5 |
> | Materially change a skill, runbook, or gate — [DOM-6]-material to future process; base class 3 | Class 3+P (effective 5) |
> | Typo fix inside a skill file — not [DOM-6]-material | 1 |
> | Class-2 fix discovers a storage-format edit is needed — a [DOM-5] risky trigger fires mid-flight | Escalate to 4 at that moment, declared |
>
> Owner: the agent starting the work declares the class; any reviewer
> may challenge it. Boundary: every unit of work from promotion of this
> section forward; explicit user instructions and safety constraints
> still rank above classification in the decision hierarchy.
> Verification: the declared class line plus the class-required
> artifacts existing; new classification guidance checked against the
> fixture table. Required action: declare the class before the first
> edit; escalate loudly the moment a trigger fires.

### Delta 2 — amend [DOM-5] opening (same file)

Replace:

> Non-trivial changes should begin with a dated plan in `docs/plans/`.

with:

> Classify the task first ([DOM-15]). Classes 3 and above begin with a
> dated plan in `docs/plans/`; classes 1–2 keep their planning record in
> the commit history or handoff report instead. The lists below remain
> the canonical trigger definitions [DOM-15] cites.

### Delta 3 — `docs/agent-context/decision-hierarchy.md`, insert before "## Required Preflight Before Edits"

> ## Classify Before the Preflight
>
> Before the repository preflight or first edit — after explicit user
> instructions and safety constraints, which always rank higher —
> declare the task class per [DOM-15] in
> `docs/specs/01-development-documentation-operating-model.md`. The
> class decides whether the full preflight below applies (classes 3+)
> or the abbreviated four-item record defined in [DOM-15]'s class-2 row
> suffices (classes 1–2 use their commit message or handoff report).
> The class is a claim; escalators are one-way and declared.

### Delta 4 — `docs/agent-context/runbooks/writing-plans.md`, append to "## File Placement"

> Classes 0–2 per [DOM-15] do not produce plan files — their record
> lives in the commit history or handoff report. This runbook governs
> classes 3 and above. Class-3+ plans carry a mandatory `Class:`
> metadata line stating the class and trigger reasoning; a post-hoc
> class claim with no mid-flight escalator history is a review smell.

### Delta 5 — `AGENTS.md`, amend the Project Conventions bullet

Replace:

> - Non-trivial changes should start with a dated plan in `docs/plans/`
>   (see [DOM-5] in `docs/specs/01-development-documentation-operating-model.md`).

with:

> - Classify every task per [DOM-15]; classes 3+ start with a dated plan
>   in `docs/plans/` (see [DOM-5] and [DOM-15] in
>   `docs/specs/01-development-documentation-operating-model.md`), while
>   classes 1–2 record their plan in the commit message, PR description,
>   or handoff report.

### Delta 6 — `docs/agent-context/engineering-principles.md`, append to §10

> The sanctioned exit is `runbooks/testing-patterns.md` Rule 5, and it
> is loud, concrete, and falsifiable — never silent. A valid substitute
> **always demonstrates the post-change correction**, and additionally
> either demonstrates the pre-change failure (or its root cause) or
> states why pre-change observation is impossible — never neither half.
> Category labels are not reasons: a docs-only change with a
> reproducible check available (a link check, a grep gate, a
> traceability run) has its failing test and must use it; a broken
> verification harness is a blocker to fix, not an exception to claim.
> Invoking Rule 5 without the demonstration is skipping the test, and
> skipping the test is not permitted at any task class.

### Delta 7 — `docs/implementation/01-documentation-system.md` (and its scaffold renderer)

Per [DOM-7]/[DOM-8], the same change updates the implementation doc: a
design-rationale paragraph (artifacts scale with class, verification does
not, and why — performative-compliance variance), a key-files row for
[DOM-15], and the change-guidance list's step 2 becomes "classify per
[DOM-15]; create a dated plan for classes 3+". The scaffold's
`render_documentation_system()` in `bin/bootstrap-agent-guidance` gets
the same edits so generated copies match. Rationale text, not normative
contract — exact wording lands at promotion, inspection-gated.

### Delta 8 — `bin/check-dom15-fixtures` (new, stdlib-only)

The structural gate for the fixture table: parses [DOM-15] from the DOM
spec; exits nonzero when a fixture names an unknown class, any class or
`+P` lacks a fixture, a class-1/2 fixture omits negative-trigger facts
("no [DOM-5]" / "intent evidence" wording), or the
cumulative-rule sentence is absent. Lands in the promotion slice (it
validates promoted text). Because it is a parser with a CLI, it gets the
repo's own floors: `--self-test` runs its four failure conditions
against embedded mutated samples (unknown class, missing class/modifier
fixture, stripped negative facts, deleted cumulative sentence) and the
adversarial-acceptance-probe basics — missing or malformed spec file →
clean invocation-error exit naming the problem; fixture-like text inside
fenced code blocks ignored; exit codes truthful in classes (0 clean,
1 contract violation, 2 invocation error); no traceback ever. Added to
the scaffold's COPIED_FILES — stdlib-only, parses the DOM spec that
consumers also receive — so the §12 gate travels with adoption.

(Delta 9 — pointer routing in secondary "non-trivial" mentions — was
removed at codex round 3: [DOM-5] owns the term and [DOM-15] maps it to
class 3, so the existing statements remain correct; sprinkled pointers
are performative routing. See §8d.)

## 5. Tasks

1. This plan revised per codex rounds 1–2 (§8a, §8b); status-index row.
   Done: both exist.
2. Codex round 3 on the revised delta — blocker for task 3. Stance: §8
   plus "do the fixtures classify consistently from stated facts now,
   and is the +P model single-format?"
3. Spec-promotion slice (strategy D, atomic): apply Deltas 1–8 exactly
   (including `bin/check-dom15-fixtures` and the implementation-doc +
   renderer updates); add this plan to the DOM spec `## Related Plans`;
   status index → `active`. Done: §6 gates pass.
4. Record the promotion baseline identifier here; backstitch rerun.

## 6. Testing Plan — exact commands

- `grep -rln "DOM-15" AGENTS.md bin/ docs/ | sort` → exactly:
  `AGENTS.md`, `bin/bootstrap-agent-guidance`,
  `bin/check-dom15-fixtures`, the DOM spec, `decision-hierarchy.md`,
  `writing-plans.md`, `docs/implementation/01-documentation-system.md`,
  and this plan (a historical record; the restatement ban applies to
  the live guidance surfaces, which carry pointers only)
- `grep -c "DOM-15" docs/specs/01-development-documentation-operating-model.md`
  → ≥ 2 (heading + [DOM-5] routing)
- `python3 bin/check-dom15-fixtures` → exit 0, after promotion
- `/Users/van/Developer/backstitch/.venv/bin/backstitch check --repo-root .`
  → `15 spec sections`, `0 errors, 0 warnings, 0 infos`
- `python3 bin/check-dom15-fixtures --self-test` → exit 0, after
  promotion (all four mutation cases caught; probe basics pass)
- `python3 bin/bootstrap-agent-guidance
  /private/tmp/claude-501/-Users-van-Developer-agent-guidance/036ce94f-f9ca-4bae-a29a-0ac11e969821/scratchpad/bootstrap-test-dom15
  --dry-run` → completes with no missing-source abort, and its output
  contains each of these exact paths (explicit presence assertions, not
  a count): `AGENTS.md`,
  `docs/specs/01-development-documentation-operating-model.md`,
  `docs/agent-context/decision-hierarchy.md`,
  `docs/agent-context/runbooks/writing-plans.md`,
  `docs/agent-context/engineering-principles.md`,
  `bin/check-dom15-fixtures`
- Inspection gate: walk the [DOM-15] fixture table and confirm each row
  classifies from its stated trigger facts under the promoted text

## 7. Verification and Gates

Per-task gates in §5–§6. Final: traceability reconciliation — spec
backlinks this plan, promotion baseline recorded, backstitch clean.

## 8. Independent Review Loop

Round 1: executed 2026-07-14 (codex, resumed session, read-only).
Verdict: blocked; 15 P1 + 3 P2 — dispositioned in §8a; revision 2 was
the response. Round 2: executed 2026-07-14, same session, on revision 2.
Verdict: blocked; 9 P1 + 1 P2, with classes 3/4 citation and DOM-11
review confirmed fixed — dispositioned in §8b; revision 3 was the
response. Review 3 (outside agent, 2026-07-14, on revision 3): verdict
"ready for round 3 with residuals" — 2 P1 + 4 P2 + 2 P3, all
dispositioned in §8c; revision 4 is the response. This review was also
the first to apply the amended [DOM-11] performative-overengineering
lens, and its structural P1 is exactly such a finding. Codex round 3
(2026-07-14, on revision 4): blocked, 6 P1 + 2 P2 — dispositioned in
§8d; revision 5 is the response. Codex round 4, scoped to verifying the
§8d fixes with the perimeter otherwise locked, must pass before task 3.

## 8c. Review Findings and Dispositions (Outside review 3, 2026-07-14)

| # | Finding (abbrev.) | Disposition |
|---|---|---|
| 1 (P1) | Class 5 auto-inherits class-4 hardening; forces fake rollback sections onto strategy-D clarifications | **Accepted — a performative-overengineering catch under the new [DOM-11] lens.** Cumulative rule split: planning/review baseline cumulative; hardening trigger-gated by [DOM-5] risk. Class-5 row, rules, invariants, and the clarify fixture updated; this plan's own header now declares `hardening: N/A` |
| 2 (P1) | Class-1 refactor fixture is the misclassification attractor | **Accepted.** Negative fixture added (two modules, unclear ownership → 3); class-1 row gains "if you had to reason about which file owns the behavior, it is not class 1" |
| 3 (P2) | Class-3 review cost will breed theater; name the allowed thinness | **Accepted.** Class-3 review may be a short structured brief (goal, class claim, invariants, verification, top risks); 4/5 keep the full bar; persona rule restated |
| 4 (P2) | Pointer surface incomplete (plans README, principles, review-loops, maintaining-traceability still say "non-trivial" unrouted) | **Accepted.** Delta 9 adds one-line routing to all four; §6 grep gate extended to match |
| 5 (P2) | Checker's bootstrap fate unstated | **Accepted.** `bin/check-dom15-fixtures` joins COPIED_FILES (stdlib-only; parses the DOM spec consumers also receive) |
| 6 (P2) | Declaration timing soft at the front | **Accepted.** Class-3+ plans carry a mandatory `Class:` metadata line (Delta 4); post-hoc claims without escalator history are a named review smell |
| 7 (P3) | Loading cards still the next gap | **Acknowledged, out of scope** (already §10) — the matrix scales artifacts, not context load |
| 8 (P3) | Fixture/DOM-5 drift needs a maintenance line | **Accepted.** "[DOM-5] edits update these fixtures in the same change" added to the fixtures paragraph |

Explicitly not reopened, per the reviewer's own recommendation:
intent-evidence rules, +P singularity, escalator design, strategy D for
clarifications.

## 8d. Review Findings and Dispositions (Codex round 3, 2026-07-14)

Verdict: blocked (6 P1 + 2 P2); hardening decoupling endorsed as sound;
both P2s are removal findings under the amended [DOM-11] lens.

| # | Finding (abbrev.) | Disposition |
|---|---|---|
| 1 (P1) | Two fixtures missing required facts (reversibility; existing-spec governance) | **Accepted.** Both rows now state them |
| 2 (P1) | Literal cumulative artifacts duplicate ceremony (class 3 would owe class-2 records too) | **Accepted.** Planning artifacts subsume; review and verification floors accumulate |
| 3 (P1) | Thin class-3 review could thin the inputs, and fresh-eyes lost its availability condition | **Accepted.** Brief is output-form only; canonical inputs and disposition loop unchanged; fresh-eyes only when no second agent is available |
| 4 (P1) | Delta 6 boolean hole (impossibility explanation could excuse both halves) | **Accepted.** Post-change correction always required; pre-change failure demonstrated or its impossibility stated — never neither |
| 5 (P1) | Checker has no firing tests for its own contract; probe floors apply to it as a parser/CLI | **Accepted.** `--self-test` with four embedded mutation cases plus probe basics (clean invocation errors, fenced-block immunity, truthful exit-code classes, no traceback) — the repo's own probes runbook applied to the repo's own tool |
| 6 (P1) | Scaffold gate verified the wrong scope with a prose count | **Accepted.** Explicit path-presence assertions replace the count |
| 7 (P2) | Delta 9 is performative routing — remove it | **Accepted — a removal finding under the new lens, overriding review-3 finding 4:** [DOM-5] owns "non-trivial" and [DOM-15] maps it to class 3, so secondary mentions remain correct; the conflict between reviewers is resolved toward the sharper principle (one owner, no sprinkled pointers) |
| 8 (P2) | Class-1 ownership sentence vague and redundant — remove it | **Accepted.** The zero-context trigger and the fixture pair carry the risk |

## 8e. Round 4 (Codex, 2026-07-14, scoped verification)

Verdict: blocked on exactly one finding — the §4 invariant still said
"each class includes the artifacts of the classes below it,"
contradicting the accepted subsume rule; the other seven fixes verified
correct. Disposition: **accepted, fixed** (invariant now reads "floors
accumulate; planning artifacts subsume; hardening is trigger-gated"),
verified by inspection. A fifth review round to re-verify a
single-sentence alignment was declined as performative under the
amended [DOM-11] lens; this note is the disclosed limitation.

## 8b. Review Findings and Dispositions (Codex round 2, 2026-07-14)

| # | Finding (abbrev.) | Disposition |
|---|---|---|
| 1 | Fixtures infer class from file topology, contradicting DOM-5 | **Accepted.** Every fixture row now states its trigger facts ("given: no [DOM-5] trigger fires", "the two sides are distinct major surfaces"); class follows from stated facts, and the table says so |
| 2 | P modeled three ways (class, modifier, treatment) | **Accepted.** `+P` is a modifier with one declaration format (`Class N+P`), effective requirements `max(N, 5)` plus pre-landing different-family review |
| 3 | Escalator restates and broadens DOM-5 | **Accepted.** Escalation re-tests the same [DOM-5]/[DOM-6] lists; the engineering warning signs force re-classification, they are not triggers |
| 4 | "Evident intent" gameable | **Accepted.** Intent evidence must be independently inspectable (spec section, explicit user requirement, existing contract test); author inference is excluded; absent evidence → class 3. Fixture pair added |
| 5 | Class-2 preflight temporally impossible | **Accepted.** Pre-edit fields (checklist, evidence, invariants, planned command) split from the completion-appended observed result |
| 6 | Executable-fixture finding unresolved; §12 has no docs-only exception | **Accepted.** Delta 8 ships `bin/check-dom15-fixtures` (stdlib, exit-code gate) checking the enumerable structure; the honest limit is stated — semantic classification is judgment verified by declared claims and review, and harness-bearing repos encode the fixtures as firing tests |
| 7 | Delta 6's exit overbroad (docs-only, infra-failure labels) | **Accepted.** Substitute proof must demonstrate pre-change failure/root cause and post-change correction or state why pre-change observation is impossible; category labels are not reasons; a broken harness is a blocker, not an exception |
| 8 | Implementation doc omitted ([DOM-7]/[DOM-8]) | **Accepted.** Delta 7 updates `01-documentation-system.md` and its scaffold renderer in the same change |
| 9 | Scaffold command not executable; dry-run flag missing | **Accepted.** §6 now has the literal command with a real scratch path and `--dry-run` |
| P2-1 | Five copied files, not four | **Accepted.** Count and list corrected in §6 |

## 8a. Review Findings and Dispositions (Codex round 1, 2026-07-14)

| # | Finding (abbrev.) | Disposition |
|---|---|---|
| 1 | One-owner rule fails: classes 3/4 restate altered DOM-5 subsets | **Accepted.** Triggers now cite "any [DOM-5] non-trivial/risky trigger" with zero restatement; escalator examples reference, not redefine |
| 2 | Class 2/3 overlap: "behavior change" vs "new behavior" | **Accepted.** Class 2 redefined as *conforming to existing intended behavior* (restoration), class 3+ as any [DOM-5] trigger; "single subsystem"/"contract" definitions dropped in favor of the DOM-5 lists |
| 3 | Class 5 circular (artifact choice, not requirement) | **Accepted.** Trigger is now "[DOM-6] **requires** a spec change, whether or not one has been drafted"; omission is a violation, not a downgrade |
| 4 | Class P omits "implemented"; doesn't resolve finding 8; class 4 too weak | **Accepted.** P now cites [DOM-6]'s full planned/implemented/reviewed/verified wording and mandates class 5 treatment — resolving the external-skill-suites finding-8 dispute in codex's favor at the spec level |
| 5 | P overbroad on surface, underbroad on substance | **Accepted.** P triggers on [DOM-6] materiality, not host surface; skill-typo (1) and material-process-in-implementation-doc (P) fixtures added |
| 6 | Class 3 weakens DOM-11 (completed-work review); inheritance implicit | **Accepted.** Class 3 review = plan and completed work; "requirements are cumulative" stated in the spec text and invariants |
| 7 | Floor codifies one side of the §10-vs-Rule-5 conflict | **Accepted — and the conflict is now resolved rather than cited around:** Delta 6 amends §10 to own its loud, named exit explicitly |
| 8 | No firing tests for [DOM-15]'s enumerable contract | **Accepted, adapted to substrate.** A 13-row classification-fixtures table is part of [DOM-15] itself; repos with harnesses must encode it as firing tests (§12); docs-only repos verify by inspection gate (§6) |
| 9 | Classes 1–2 can't prove pre-edit declaration; commits may be unauthorized | **Accepted.** Declaration is made in-session before the first edit and *recorded* at landing; the handoff report is the sanctioned uncommitted home, matching AGENTS.md's uncommitted-review path |
| 10 | Class 1 contradicts Delta 3; "observed result" can't exist at planning time | **Accepted.** Delta 3 reworded (abbreviated record, not "no artifact"); class 1 artifact is a completion record; the plan-vs-record distinction made explicit |
| 11 | Class 2 abbreviated preflight undefined | **Accepted.** Enumerated: outcome checklist, governing spec or `Source spec: None`, invariants, verification command + result |
| 12 | "Unit of work" undefined; decomposition laundering | **Accepted.** Defined as the whole requested outcome; slices inherit the minimum class; stated in spec text and invariants |
| 13 | File-count disposition not fully honored (new tests smuggled in) | **Accepted.** Class 1/2 definitions rebuilt on observable-behavior and intent-conformance, not boundary counts or subsystem counts |
| 14 | Wrong plan type/strategy (B vs D) | **Accepted.** Plan type spec-authoring, strategy D |
| P2-1 | Spec clarification has no class | **Accepted.** Clarification-only normative edits are class 5 with strategy D, in the class-5 row and fixtures |
| P2-2 | "Before anything else" too broad | **Accepted.** "Before the repository preflight or first edit," with user instructions and safety explicitly above |
| P2-3 | Verification commands unspecified | **Accepted.** §6 now names exact commands, expected outputs, and the grep scope for the restatement ban |

## 9. Assumptions and Open Questions

- (Resolved by round 2, finding 4: intent evidence must be independently
  inspectable; absent evidence → class 3.)
- Whether sibling repos need class-trigger tuning is deferred to
  propagation evidence. Reopens on systematic misclassification.
- `bin/check-dom15-fixtures` checks structure, not judgment; if round 3
  finds the structural checks too weak to count as the §12 gate, the
  fallback is encoding the fixtures as a golden classification file the
  checker diffs. Owner: round-3 reviewer.

## 10. Out of Scope

- Status vocabulary; kernel context budget; loading cards; provenance
  stamp
- Reclassifying existing plans
- Propagation (rides with coalescing propagation)

## 11. Fresh-Eyes Review

Revision 3 checked: fixtures classify from stated trigger facts, never
topology, and cover both sides of each boundary codex found ambiguous
(intent-evidence present/absent; producer-consumer with/without a
surface-crossing fact); `+P` has exactly one model and one declaration
format; escalation adds no triggers; class-2's record is temporally
coherent (pre-edit fields, completion-appended result); the §12 gate is
executable (`bin/check-dom15-fixtures`) with its judgment limit stated
rather than hidden; Delta 6's exit demands demonstration, not category
labels; the [DOM-7]/[DOM-8] alignment and scaffold renderer ride in the
same change. The plan classifies itself Class 5+P and still blocks its
own promotion on round-3 review.

Revision 4 additionally checked: hardening is trigger-gated, not
inherited, and the plan's own header exercises the `hardening: N/A`
declaration; the class-1 refactor attractor has a negative fixture and
an ownership sentence; class-3 review thinness is named so the theater
risk has a sanctioned honest form; all four remaining "non-trivial"
surfaces route through [DOM-15] with pointers, not restatements; the
checker travels via COPIED_FILES so §12 holds beyond this repo.
