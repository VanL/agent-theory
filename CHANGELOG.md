# Corpus Changelog

Dated, human- and agent-comparable record of normative changes to the
agent-theory corpus. Consumers compare their adoption/propagation pin date
against this file to detect staleness cheaply before deciding whether a
propagation wave is worth running; the SHA pin remains the authoritative
provenance (`skills/propagate-guidance/SKILL.md` step 0).

## 2026-10-15 (whole-plan review lenses, test-audit skill promotion, and taste-up-front boundary)

- **Whole-plan review lenses** (`docs/specs/01-development-documentation-operating-model.md` `[DOM-11]`, `docs/agent-context/engineering-principles.md` §8, `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md` §3–§4, `docs/agent-context/runbooks/writing-plans.md` §8 & §10, and `skills/call-agent/SKILL.md` §2):
  - Plan reviews evaluate the plan as a whole, including all amendments, through two explicit lenses in addition to point-defect checks: (1) is this what an expert developer would do and think well-crafted or elegant? (2) is there a known algorithm or computer science principle that should be applied here?
- **Promoted `skills/test-audit/` (`SKILL.md` and `SWEEP.md`)** (`skills/README.md`, `docs/README.md`, `docs/implementation/02-repository-map.md`, `docs/agent-context/runbooks/external-skill-suites.md`, and `bin/bootstrap-agent-theory`):
  - Two-part test-suite quality audit and single-file execution guide ported from SimpleBroker (`f18b9c6` / `5410aff`), generalized for the ecosystem with the October 2026 contention-witness vs stress-budget boundary folded into `Exercise Production Behavior` and `Junk Patterns`.
- **Communicating program feel ("taste up front") vs. BDUF** (`docs/program-theory.md` `[REV-AT-005]`, `docs/specs/02-agent-theory-and-program-theory.md` `[AT-REF-2]` & `[AT-REF-4]`, and `skills/crystallize-program-theory/SKILL.md` spine Q2, Q5, and §4):
  - Clarified that encoding intrinsic feel, command/API grammar, and core composable operations up front with concrete "taste anchors" belongs in `docs/program-theory.md` and is distinct from Big Design Up Front (locking in premature internal schemas or building horizontal framework layers in isolation).
- **2026-10-14 propagation wave adaptation back-ports (`b6f2141`)**:
  - `AGENTS.md`: module-theory rules pointer directed to `[DOM-2]`, `[AT-REF-4]`, and `skills/crystallize-program-theory/SKILL.md`.
  - `skills/crystallize-program-theory/SKILL.md`: attributed `[AT-THEORY-*]` citations to the `agent-theory` hub paired with local `[AT-REF-4]`.
  - `docs/agent-context/engineering-principles.md` §14: clarified that a governance or policy-checking tool may never exempt or suppress its own policy check on itself.
  - `skills/coalescing/SKILL.md` step 3.4: distinguished `git cat-file -e` object verification from `git merge-base --is-ancestor` retained-ref reachability and `bin/coalesce-check` remote-ancestry checks.
  - `skills/propagate-guidance/SKILL.md` step 4: recorded adaptation notes for uncrystallized `docs/program-theory.md` repositories and `bin/coalesce-check` shallow-clone ordering.

## 2026-10-14 (five-repo ecosystem fold-up wave)

Cross-repository fold-up wave across `simplebroker` (`8a5578a`), `taut`
(`f4275a6`), `weft` (`9b7ada69`), `backstitch` (`7d627f3`), and `mm`
(`16d96241f`) per `docs/plans/2026-10-14-ecosystem-fold-up-wave-plan.md`
(Class `5+P`):

- `docs/specs/01-development-documentation-operating-model.md`:
  - `[DOM-10]`: verification commands must match the exact CI collection roots,
    markers, and working directories; delegated RED-phase claims require
    parent-agent transcript verification before dispatching GREEN.
  - `[DOM-11]`: three-tier review hierarchy — Tier 1 cross-family external CLI
    review (`skills/call-agent/SKILL.md`), Tier 2 native-subagent fallback only
    after two bounded, logged Tier-1 attempts fail (recorded as
    `same-family fallback (degraded)`), Tier 3 fresh-eyes self-review when no
    second agent is available (recorded with `Review: unavailable — <reason>` on
    Class ≥3 plans); `RECONSIDERATION REQUESTED` disposition when a finding
    collides with a standing boundary; `fixed in plan` dispositions must match
    actual plan task body edits; P1 fixes name the single-line production
    mutation that fails the new test.
  - `[DOM-14]`: graduated three-tier fold verification (`text fidelity`,
    `symbol liveness`, `behavioral parity`, with a lightweight doc-only floor);
    bounded in-sweep maintenance; noncontiguous lesson fold records when
    reclassification breaks monotonic date cursors; revision markers placed
    after `- YYYY-MM-DD:`.
- `docs/program-theory.md`: `[AT-THEORY-4]` item 4 ("Deliberate friction
  replaces lost social friction") enriched with the speed-vs-review social
  friction formulation (`simplebroker` `f18b9c6`).
- `AGENTS.md`: subagent authorization scoped to research, exploration,
  supervised implementation slices, and Tier-2 fallback reviews after recorded
  Tier-1 unavailability; delegated RED transcript verification rule.
- `docs/agent-context/principles.md`: returning mid-task when investigation
  falsifies a task's premise (`weft` `ff91368e`); affirmative full-tree grep
  evidence required before applying negative lifecycle labels (`unused`,
  `dead`, `orphaned`, `stale`, `superseded`).
- `docs/agent-context/decision-hierarchy.md`: mechanical count and completeness
  verification (`all`, `every`, `full`, `zero`) in the Completion Gate.
- `docs/agent-context/engineering-principles.md`:
  - §2: non-default resolved configuration tested through the inner runner.
  - §4: repeated contention/retry-budget tuning as a theory-possession
    stop-condition; module-owned clock/platform helper seams.
  - §8: cross-family review vs same-family framing bias; three empirical
    review checks (`causal premise in code`, `falsifiable proof`, and
    `empirical identifiers by command`); `RECONSIDERATION REQUESTED`;
    disposition-vs-body sync check.
  - §10: handshake/protocol peers declare expected wire literals independently;
    release-lineage fixtures generated through prior release code or frozen byte
    snapshots.
  - §11: `"unused"` and dead-code audits search `examples/`, bootstrap scripts,
    and vendored consumers before removal.
  - §12: mechanical verification of numeric and completeness claims (`"full"` is
    made true, not weakened to `"core"`).
  - §14: static complexity thresholds as visibility signals, governed
    suppression registries paired with state-machine contracts, zero
    self-suppression in governance tools, and real-config linter probes.
- `docs/agent-context/runbooks/`:
  - `review-loops-and-agent-bootstrap.md`: Tier 1/2/3 hierarchy, premise/
    falsifiability review duty, brief element 7 (standing boundaries + refused
    alternatives), `RECONSIDERATION REQUESTED`, and `fixed in plan` body sync.
  - `writing-plans.md`: mechanical count verification, falsified-premise return
    rule, paragraph-level spec scope + removed-paragraph hazard audit (§4c),
    review protocol metadata + placeholder guard (§8), graduated
    `Reviewed baseline:` pin + `## Revision Log` table, and explicit rejection
    of status-column deployment prose qualifiers.
  - `testing-patterns.md`: Rules 7–10 (independent wire literals + release
    fixtures, boundary straddling + non-default inner config, reachable
    negative setup + producer closure, test-deletion equivalence owner),
    Pattern 9 (contention reduction, negative timing windows, shared-module
    patching), and Verification Pattern updates.
  - `hardening-plans.md`: §1 standing invariants surface reconciliation and
    simplification difference register; §13 planning duty to name and verify
    the owning product cleanup contract and liveness preconditions; §15 planning
    duty to name how publication guards against verified remote state going
    stale during long test suites and how that guard's failure path is verified
    before publication.
  - `writing-specs.md`: inline traceability directives (`_Traceability: meta_`
    / `_Traceability: ignore <reason>_`) and removed-paragraph hazard audit on
    spec extraction/simplification.
  - `maintaining-traceability.md`: exact CI-root verification and `tests/`
    backlink grep before converting plan backlinks to `- retired:`.
- `skills/`: updated `call-agent/SKILL.md` (Tier-2 fallback rule + brief element
  7), `coalescing/SKILL.md` (three-tier verification, `- YYYY-MM-DD: (revised
  ...)` ordering, in-situ version qualification vs expiry, all-eligible plan
  sweep rule + test backlink grep, noncontiguous lesson fold records), and
  `debugging/SKILL.md` (boundary straddling, P1 mutation line, contention
  stop-condition).
- `bin/` & `.github/workflows/gates.yml`:
  - `bin/check-doc-paths`: fenced-code-block stripping (`_prose_lines()`),
    governed `DECLARED_FUTURE_ARTIFACTS` with two-way honesty checks, and
    `--self-test` mode (wired in CI).
  - `bin/check-dom15-fixtures`: broadened `NEGATIVE_FACT_PATTERNS`, positive
    trigger check (`states_firing_trigger()`), and mutation probes for
    unclosed fences and hidden triggers.
  - `bin/coalesce-check`: dynamic default-branch detection
    (`resolve_remote_ref()` via `origin/HEAD` with `origin/main` fallback) and
    `## Retired Plans` cue verification (`retired_plan_cues()`).
  - `bin/bootstrap-agent-theory`: fixed duplicate step `3.` numbering in
    `render_documentation_system()`.
- Human-facing readability & paragraphing pass (`README.md`, `docs/README.md`,
  `docs/specs/02-agent-theory-and-program-theory.md`, `docs/program-theory.md`,
  `docs/implementation/01-documentation-system.md`, `[DOM-2]`/`[DOM-5]`, and
  `docs/agent-context/decision-hierarchy.md`): clarified topic sentences,
  added an end-to-end 6-step workflow walkthrough in `README.md`, split
  multi-topic paragraphs, and replaced abstract nominalizations with active,
  STE100-aligned prose while preserving all diagnostic vocabulary, reference
  codes, and normative clauses (verified by `codex` Rounds 4–5).
- `docs/agent-context/context.index.yaml`: updated `updated_at` to `2026-10-14`.
- Shared-worktree additions landed in the same commit: `docs/lore/` (dated
  primary-source records, registered in `docs/README.md` and
  `docs/implementation/02-repository-map.md`), `skills/crystallize-program-theory/SKILL.md`
  (nine-item owner possession checklist for product apex theories),
  `docs/agent-context/principles.md` ("Report surprise; do not absorb it"), and
  `docs/plans/2026-08-11-plan-metadata-gate-plan.md` (`draft` plan and status-index
  entry).

## 2026-08-07 (ascension boundary)

- `docs/program-theory.md`: [REV-AT-004] — admission to the hub has
  two screens: the admission test (real practice) and the ascension
  boundary (a generalization of the discipline itself). The hub
  generalizes the discipline; product theories generalize the
  products; recurring product-engineering rules are evidence for
  product theories, never fold-up candidates. [AT-THEORY-7] gains
  "What ascends here (and what does not)".
- `skills/coalescing/SKILL.md` step 5 and the fold-up threshold row:
  "generalizes" scoped to the discipline at the point of proposal.

## 2026-08-07 (gate-wiring wording clarified)

- `writing-specs.md`: the gate-wiring obligation is a **declared
  execution path** — CI where wired, explicit manual execution
  otherwise — not CI for every tool. Owner-directed after the taut
  landing showed the prior wording false-flagging deliberate manual
  sweep/propagation tooling. Back-ported to SimpleBroker in the same
  session; taut already carries the corrected form.

## 2026-08-07 (maintenance classification generalized)

- [DOM-15] Rules, [DOM-14], `skills/coalescing/SKILL.md`: ordinary
  maintenance under an existing procedure defaults to Class 2 when
  reversible and intent-evidenced; it escalates only on an explicit
  change to ongoing procedure or durable guidance, or an independent
  trigger. Durable-guidance promotions gate on the **human owner**;
  agent review supports but never substitutes (owner decision
  2026-08-07).

## 2026-08-07 (retirement verification relaxed)

- [DOM-14], `writing-plans.md` Plan Lifecycle, `skills/coalescing/SKILL.md`
  step 3.4: second-agent verification before physical plan deletion is
  now optional, not required — deletion of source-pinned plans
  reachable from a retained ref is reversible archive maintenance
  (owner decision 2026-08-07). Still required: re-checking the
  recorded harvest gate from the current tree, verified retrieval from
  the source SHA, ref reachability, and two-step sequencing
  (soft-retire in one change, delete in a dedicated follow-up).

## 2026-08-07 (register-conditioning adoption)

- `docs/program-theory.md`: [REV-AT-003] adopted — guidance artifacts
  carry a working register as well as propositions; composing
  always-loaded surfaces (including citations) is a
  capability-environment decision. Includes the experiment-status
  statement (hypothesis, evidence deficit, standing falsifier) and the
  direction-free Pressure record; register remains non-evidentiary.
  [AT-THEORY-6] gains the register-without-transfer falsifier.
- `skills/crystallize-program-theory/SKILL.md`: citation tests for
  theory drafting — accurately represented and load-bearing; register
  effects are drafting hypotheses, never evidence.

## 2026-08-07

Backport wave from the SimpleBroker testbed (pin `a38e6a9`; plan
`docs/plans/2026-08-07-simplebroker-backport-wave-plan.md`, three-round
independent review):

- **Scaffold contract change:** `bin/coalesce-check` now detects
  shallow clones and skips the SHA-resolution/retrieval-cue legs loudly
  with exit 0 (previously: false BROKEN, exit 1); non-SHA counts still
  print. Enforcement CI must use full history.
- `docs/specs/01-...operating-model.md`: [DOM-5] git-backed coalescing
  carve-out (routine retained-ref sweep is Class 2, not a destructive
  edge; guidance promotion still escalates); [DOM-14] additive-first
  bullet replaced by the archive rule (worktree-only material stays
  ineligible); [DOM-15] fixture table +2 sweep rows. Owner-ratified
  (OD-1).
- `AGENTS.md`: program theory declared load-bearing for product-scope
  judgment (audits, reviews, design opinions), gated in CI;
  session-start coalescing check cue; status-index row required at
  class 3+ creation and flipped at completion (also in Definition of
  Done and `writing-plans.md`).
- `context.index.yaml`/`agent-context/README.md`: read_order repaired —
  the three read-order statements now match element-for-element, gated
  by a structural CI comparison.
- `writing-specs.md`: theory boundary (specs may refine, not silently
  contradict, theory; theory may not duplicate exact behavior);
  gate-wiring rule (every gate names its CI path; history-dependent
  gates skip loudly on shallow clones).
- `writing-plans.md`: existence-check-before-review duty (author side;
  reviewer side in `review-loops-and-agent-bootstrap.md`, promoted by
  owner direction OD-4); comprehension-gate teeth (expected answers in
  plan, answers in execution log, wrong answer blocks); supersession
  and completion index flips; git-backed retirement is routine
  maintenance; source SHAs must be ref-reachable ("a loose object is
  not a durable archive"); demotion-in-place of superseded plan text
  (promoted by owner direction OD-2).
- `review-loops-and-agent-bootstrap.md`: existence-check-first reviewer
  duty; guidance surfaces are reviewable and blockable; deferred-units
  register with reopen conditions and severance check; audit-response
  protocol (§5a, conditional on large/systemic audits); review-timeout
  calibration clause.
- `hardening-plans.md`: §15 release stop-gates (driver outranks prose;
  rerun gates from the release identifier; publish only after
  exact-identifier green; per-identifier recovery; honest rollback;
  artifact-based post-release acceptance).
- `maintaining-traceability.md`: chain terminus is code **with** test
  evidence; closure review diffs every planned task against executable
  evidence (a gated-off test is not evidence).
- `testing-patterns.md`: Pattern 8 — multiprocess coordination needs
  aggregate deadlines; serialization groups constrain only their own
  members.
- `writing-implementation-docs.md`: do not copy non-goals or capability
  limits into implementation docs; link the owning theory or contract.
- `skills/coalescing/SKILL.md` + `docs/coalescing.md`: Unindexed
  threshold tier (any positive reportable); durable-guidance ceiling
  inside sweeps; archive-phase rename with retained-ref conditions;
  additive watermark rule; consolidated report-when list;
  `coalesce-check` stated as evidence trail, not a second recipe (the
  state file wins on disagreement).
- `skills/brainstorming-to-plan/SKILL.md`: four-part admission test for
  durable rejected alternatives (adaptation from the pin).
- `docs/lessons.md`: Golden Rule 14 — the lessons ledger is itself a
  reviewable surface.
- `docs/coalescing.md` fold-up ledger: demotion-in-place graduated by
  owner direction; Revision Log + reviewed-baseline pin held with SB
  partial family evidence; eight-candidate SB slate registered at one
  lineage.
- `bin/check-dom15-fixtures`: rigorous fence parser (nested-fence
  probe added red-first; fence probes now routed through the real
  extraction path); CI runs live check and `--self-test` as separate
  steps.
- `bin/check-doc-paths`: recorded negative knowledge on guidance-only
  scan roots; adopter note for extending `SCAN_FILES`.

## 2026-08-06

Testbed feedback from the simplebroker adversarial audit and remediation
(2026-08-05/06):

- `runbooks/writing-specs.md`: authoring-time rule — adding or editing a
  normative enumerated list lands its executable gate in the same change (or
  names a judgment floor); matching anti-pattern added.
- `engineering-principles.md` §12: recursion floor — gates do not gate
  gates; verification chains terminate in a declared claim plus independent
  review.
- `runbooks/testing-patterns.md`: Pattern 7 — a test must not neutralize the
  hostile default environment it claims to cover (forced unbuffering,
  oversized payloads, generous timeouts).
- `runbooks/review-loops-and-agent-bootstrap.md`: different-family review
  attempts are bounded (default two), timed out, and recorded in the plan's
  review log before same-family fallback; "not available" is evidenced,
  never asserted.
- `docs/program-theory.md`: possession probing recurs — one probe per
  release or class-5 plan completion, recorded.
- `docs/agent-context/README.md`: read-order compliance declared as a
  declared-claim floor for product-scope judgment, checked by review.
- `docs/coalescing.md`: non-gating apparatus-share reporting cue.
- `skills/propagate-guidance/SKILL.md`: dogfood sweep — each waved rule is
  applied to the hub's own surfaces in the same session.
- Introduced this changelog as the corpus staleness signal.
