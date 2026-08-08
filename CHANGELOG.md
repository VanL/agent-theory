# Corpus Changelog

Dated, human- and agent-comparable record of normative changes to the
agent-theory corpus. Consumers compare their adoption/propagation pin date
against this file to detect staleness cheaply before deciding whether a
propagation wave is worth running; the SHA pin remains the authoritative
provenance (`skills/propagate-guidance/SKILL.md` step 0).

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
