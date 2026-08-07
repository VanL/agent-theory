# Lessons Learned

Use this file for durable, project-level lessons that should influence future
sessions.

Startup context is the Golden Rules plus entries after the watermark in
`docs/coalescing.md`; the rest of this ledger is searchable history.

## When To Add A Lesson

- A correction exposed a repeated failure mode.
- A missing document or runbook caused rework.
- A plan or spec was too ambiguous to execute safely.
- A completed change revealed a stronger general rule than the repo previously
  encoded.

## Golden Rules

Universal principles that inform every change. The dated section below is the
incident log; these are the durable rules distilled from it.

1. **Canonicalize once, at the boundary.** Normalize data at ingest and write
   boundaries through one shared helper. Never add runtime dual-case fallback
   readers — they hide contract bugs.
2. **Fix forward, never fall back.** Do not add read-time fallback modes to mask
   drift or corruption. Detect invariant violations and surface them; repair with
   forward migrations.
3. **One canonical contract across all consumers.** Same keys, shapes, and
   vocabulary everywhere. Mixed legacy keys cause cascading mismatches.
4. **Validate at write time, fail fast.** Catch errors at the point of creation,
   not in downstream batch gates or runtime checks.
5. **Update all consumers in the same change.** When renaming keys, tightening
   schemas, or changing contracts, update all producers and consumers together.
   Partial renames pass isolated checks but fail at runtime.
6. **Test what you ship.** Add a regression test with each behavior-changing fix.
   Generate fixtures through production code paths, not synthesis.
7. **Plans fail at boundaries, not in the middle.** For risky work, name what
   must not change, hidden couplings, anti-mocking rules, rollout and rollback
   constraints, and post-deploy success signals before implementation starts.
8. **If a document is human-clear but agent-ambiguous, tighten it immediately.**
   Missing owner, boundary, verification path, or required action makes agents
   guess wrong even when the prose feels obvious to a human.
9. **Agents suggest dependencies; humans add them.** An agent must not introduce a
   new dependency on its own — propose it with justification (purpose, why the
   standard library or an already-vendored dependency will not do, cost of taking
   it on). The human decides whether it enters the manifest.
10. **Flag concerns and calibrate uncertainty, even when you did exactly what was
    asked.** Surface risks noticed in passing; distinguish verified from
    unverified claims with precise language ("I have not confirmed X") rather than
    a vague "this should work"; report blockers with precise causes.
11. **Handle the error path, not just the happy path.** A feature whose success
    path works but whose error, empty, or timeout path is silently ignored is
    incomplete. Name the failure cases in the plan and test at least one. Do not
    paper over an unexpected null or empty — find out why first.
12. **Formatting is owned by the project formatters — run them; do not hand-format,
    and do not reformat incidentally.** Let the tools decide style; in a behavior
    change keep the diff to the lines the task requires and do not let a formatter
    reflow untouched code; keep formatting-only churn in its own change; if a line
    changed only because "I was in there," revert it.
13. **Enumerable contracts get executable gates.** Any list a document asserts
    — issue codes, exit codes, edge cases, config keys — must be mirrored by a
    machine check that enumerates it (a firing test per element, a no-op
    prevention test per key). Prose binds only what gets checked; agents
    comply uniformly with gates and unevenly with everything else. (See
    engineering-principles §12 and testing-patterns Pattern 6.)
14. **The lessons ledger is itself a reviewable surface**, not a place
    confident text lands unreviewed — an entry can teach a disproved
    protocol as durable guidance hours after drafting. An uncommitted
    entry corrected in place owes no supersession ceremony; the ceremony
    is owed after landing. (From SimpleBroker's pre-release cycle, its
    `docs/lessons.md` at pin `a38e6a9`.)

## Lessons

- 2026-07-14: Two staging-safety rules from the weft landing. (1) A
  blocking pre-commit check must actually halt the whole script — an
  `if/else` that skips only the commit lets the script tail run
  `git commit` again with the full index and sweep it into a mislabeled
  commit (recovered via `git reset --soft`). (2) Content greps for
  foreign WIP false-positive on the plan's own dirty-tree invariant,
  which names those files; the reliable gate is **staged-file-list
  equality** against an explicit expected list, plus synthetic HEAD+mine
  blobs for shared-dirty files. Also: blanket token replacement in
  transplanted prose needs a readability pass, not just a
  zero-leftovers assertion — five garbled sentences shipped past the
  assert and were caught only by independent review.
- 2026-07-14: In multi-repo sessions, `cd` persists across `&&` within a
  shell call: a `git add -A && git commit` intended for one repo executed
  in another and swept 53 files of a sibling's uncommitted WIP into a
  mislabeled commit (recovered via `git reset HEAD~1`, worktree
  untouched). Rule: every repo-mutating git command in a cross-repo
  session names its repo explicitly (`git -C <repo>` or a fresh `cd` in
  the same command), and `git add -A` is banned in repos with foreign
  WIP — stage by explicit path list, then grep the staged diff for
  foreign markers before committing.
- 2026-07-15: Runbook code examples are claims too. A fold that
  distills lessons into a runbook should also verify the runbook's
  *pre-existing* examples adjacent to its edits — an mm fold found a
  patch-target example that would `AttributeError` on contact (the
  named modules import the symbol function-locally; the canonical
  owner lives elsewhere), sitting in the exact pattern the incoming
  lesson warned about. Discovered by a delegated Opus fold that tested
  the runbook against the lesson it was placing; my five prior folds
  verified lessons against code but never audited existing examples.
  Third tier-3 companion rule; promote into the coalescing skill with
  the other two at the next guidance touch.
- 2026-07-15: Lessons that encode upstream framework facts (not house
  choices) carry a decay clock bound to the dependency version, not to
  doc coverage. When the pinned version makes the violation impossible
  or loudly self-failing (mm: `django.utils.timezone.utc` removed in
  Django 5.0, pinned 6.0.7 — any use raises at import), the lesson has
  **expired**: fold to git with the version fact as the cue, no
  distillation target owed. Still-live framework facts are platform
  documentation, not conventions — they scatter to the nearest topic
  doc rather than justifying a "our conventions" home. Owner insight
  ("it's not our conventions — Django changed") from the mm Django/DRF
  fold; fold-up candidate for [DOM-14]'s decay guidance alongside the
  citation-driven decay rule.
- 2026-07-15: A coalescing fold's verification has three tiers, and only
  the first two are automatic: text fidelity (lesson → distillation,
  grep both directions), symbol liveness (named functions/files/flags
  still exist), and **behavioral parity** (the code still does what the
  rule claims). The third is mandatory whenever a distillation is
  phrased as a current-behavior claim — especially present-tense text
  landing in implementation docs, which by the claims-vs-evidence rule
  is a status claim requiring reproduction. The mm Containers/CI fold
  shipped ten such claims verified only to tier two; an owner question
  forced tier three (all ten reproduced, one apparent drift resolved as
  the rule's own blessed fallback case). Candidate for the coalescing
  skill after a second section confirms the pattern.
- 2026-07-15: A true-negative validates the check, not the phenomenon —
  it does not mint fold-up lineage. Weft ran the framework-fact expiry
  check at a real pin bump, zero expiries fired; the drafting agent (who
  saw only the doc surfaces) recorded "no check ran," and the reviewer
  correctly held the [DOM-14] decay-bullet graduation either way: a spec
  should not impose duties on branches of a conditional that only one
  repo has ever exercised. Two rules. (1) Lineage requires the *required
  action* to have fired — an incident, or a durably installed local
  method — not a one-shot hypothesis probe that returned clean. (2)
  Cross-repo evidence must live in the durable run log, not only a
  commit message: the weft evidence was commit-message-only, which is
  exactly why the drafting pass mis-recorded it (both errors were real —
  weft under-recorded, the drafter over-concluded).
- 2026-07-28: **Two fold-ups from taut's local method evolution** (its
  commit `3706d73`, accepted by owner direction). (1) *Repair-in-sweep*:
  an authorized sweep is maintenance as well as compaction — inspect the
  memory surfaces before trusting a count; repair in-wave when the
  defect is in-boundary, reversible, and evidence-determined; merely
  logging a repairable defect is not a completed sweep (1 durable
  lineage — this week's hub/weft ad-hoc repairs share ancestry with the
  triggering review and were not counted). (2) *Structured status-index
  contract*: closed vocabulary with a `status-review` quarantine that
  never counts as completed, an executable index gate whose failure
  blocks derivation, and never-fall-back-to-free-form-headers (2
  lineages: taut built the mechanism; mm's backfill independently
  invented the quarantine as free text — "unknown, needs owner triage").
  Convergence note: taut built its §12-style executable gate the same
  day the hub built check-doc-paths/coalesce-check, uncoordinated — two
  repos independently concluding the corpus must check its own claims.
- 2026-07-30: **A doc edit reclassifies upward the moment it changes read
  order, changes a renderer, or names a concept other repositories will
  copy.** The program-theory work was scoped and executed as documentation
  and acquired all three properties without anyone re-running [DOM-15];
  the governing plan was written retrospectively
  (`docs/plans/2026-07-30-program-theory-and-module-theory.md`). The
  trigger is stated as three checkable properties rather than "feels
  bigger now" precisely because the misjudgment happens at the start,
  when the work genuinely is a doc edit. Corollary for the retrospective
  plan itself: write it in its true tense — its rejected-alternatives
  section is the only part that carries information the artifact cannot,
  and a retrospective plan dressed as a prospective one is the ceremony
  the admission test rejects.
- 2026-07-30: **Do not freeze plan index or review sections as durable
  evidence of transient state.** The program-theory plan still said
  "uncommitted" and "review pending" after `4acbad1` landed on `main` without
  pre-landing +P review. Independent review after the fact is valid only if
  the repository records the order honestly (baseline SHA, deviation, no
  backfill that review preceded the commit). Same family as
  plans-record-evidence: status prose is a claim; `git log` is evidence.
- 2026-07-30: **Scaffold identity is a semantic contract, not only path
  claims.** Copying hub entry docs that say "this hub repository" / "what
  agent-theory is" into a product repo creates a category error the
  program-theory stub cannot fix. Prefer scope-neutral entry language plus an
  assertion over ever-more substitutions in the bootstrap adapter.
- 2026-07-17: **Propagation transplants come from the pinned end-state,
  never an intermediate commit's diff.** A wave range can contain a
  change and its own later amendment; extracting from the authoring
  commit lands text the hub already walked back (the taut wave worker
  transplanted a reverted verdict-vocabulary change from `cd74fcd`,
  missing `6052289`; caught by orchestrator pre-review and the repo's
  scoped review). `git show <pin>:<path>` is the only extraction form.
  Companion observation from the same wave: the
  plans-record-evidence rule caught transient-state prose in three
  different repos' wave plans on its first day — a form-level rule that
  fires that reliably is doing spec-grade work.
- 2026-08-06: **A doctrine that has not been self-applied drifts first on
  the corpus's own surfaces.** The simplebroker audit/remediation cycle
  showed §12's enumeration rule, the review-fallback order, and the
  read-order requirement all existed as written doctrine while the hub's
  own spec-writing, review, and session-start surfaces went unchecked
  against them — a remediation that ran fourteen review rounds still
  shipped a fresh ungated enumeration, because nothing applies gates to
  the spec-*writing* act. Fix pattern: when a rule is added, sweep the
  hub's own specs, runbooks, and skills for surfaces it binds in the same
  change (now the dogfood step in `skills/propagate-guidance`), and write
  each new doctrine with its floor named (gate, or declared claim plus
  review — never neither).
- 2026-08-06: **A well-formed plan is not a verified plan; form fluency
  carries no information.** Agent-authored plans reproduce every
  hardening artifact — invariants, stop gates, anti-mocking clauses,
  deviation logs — while naming nonexistent surfaces and proposing
  deadlocks with identical confidence. In one simplebroker pre-release
  cycle, a plan carrying full hardening form cited a CLI flag that does
  not exist (`--since`), a test seam that does not exist (`evalsha`),
  a wrong race-gate test file, and a release order that contradicted the
  executable driver — across two review rounds. Review rule: before
  grading anything else, existence-check every named flag, test path,
  seam, and driver order against executable code; the round-1 reviewer's
  formulation ("when a plan names an existing release or CI driver,
  compare its proposed order and collection roots to executable code
  before accepting prose claims") generalizes to all named surfaces.
  Candidate for a normative line in the writing-plans/review runbooks
  once cited from a second repository. (From simplebroker's
  "2026-08-06-pre-release-review-remediation-plan", rounds 1–2.)
- 2026-08-06: **Fixes touching a lock order, object lifecycle, or
  registered concurrency state machine are architectural regardless of
  diff size — classify by surface, not lines.** Three of five "small
  code debts" in the same simplebroker plan, each an apparent
  one-liner, were: a PostgreSQL lock-order cycle (advisory→meta vs
  meta→advisory across alias operations), a reentrant self-deadlock
  (a broadcast path delegating into an insert path under the
  newly-shared non-reentrant lock), and a structural impossibility (a
  GC finalizer for an object its own thread target strongly retains).
  Diff-size intuition classified all three as hygiene; the [DOM-5]
  trigger lists classified them correctly once the surface was named.
  Candidate for an explicit note beside the [DOM-15] fixtures once
  cited from a second repository. (Same plan, findings F6–F8.)
- 2026-08-06: **A refusal recorded in a closed plan does not transfer,
  even when the next proposer reads and cites it.** simplebroker's
  2026-07-13 investigation recorded precisely why cross-thread
  generator cleanup could not be repaired (foreign threads cannot own
  the rollback, the lock release, or waiter wakeup); the next design
  cycle cited that record and still re-proposed repair as "healing,"
  costing four adversarial review rounds before the refusal was
  promoted to a theory-tier revision record — after which the category
  error became unwritable. Failure mode: incident-tier storage reads
  as "that specific fix was rejected," not "this category is a
  category error." Rule: record a refusal, with its why, at the tier
  the next proposer loads before judgment (theory revision, golden
  rule, or session ledger) — not only where the rejection happened.
  (From simplebroker's generator-poisoning arc, plans of 2026-07-13
  and 2026-07-27.)
- 2026-08-06: **Register symmetry: how a context is written raises output
  quality and error camouflage together.** Prompt and corpus register
  condition which region of an agent's capability is evoked — engaging at
  the top of one's ability, and loading corpus prose written at that
  level, evokes matching-level output. But register conditions *form*
  directly and correctness only indirectly, so high-register engagement
  also produces high-register wrongness that matches the very fluency
  heuristic the reader uses for quality. This is the mechanism under "a
  well-formed plan is not a verified plan": the simplebroker pre-release
  cycle produced deadlock proposals and nonexistent surfaces in prose
  indistinguishable from its correct output. Operational consequences,
  already doctrine, now with their why: register is never evidence
  (mechanical existence-checks and gates grade correctness);
  cross-family review works partly because fluency biases differ across
  model families; and the always-loaded corpus is a register instrument,
  not only an information store — it institutionalizes the owner's best
  engagement as ambient conditioning. (From the simplebroker
  "2026-08-06-pre-release-review-remediation-plan" review cycle and the
  owner dialogue distilling it.)
- 2026-07-17: **Commit subjects must name the largest-impact change in
  the diff.** Contract, authority, or architecture changes never ride in
  a commit named for something else — the log is a human review surface,
  and a mislabeled commit hides its diff from the reviewer who trusts
  subjects. Observed benignly at weft ("Update deps" carrying the
  simplebroker pin bump that later mattered for lineage evidence) and
  harmfully at mm (the July 2026 lifecycle inversions traveled inside
  omnibus subjects). Two independent lineages; candidate for
  engineering-principles once cited from a third context.
- 2026-07-14: Capture an external reviewer's full transcript to a file
  before filtering or truncating stdout (`tee` first, filter after). The
  mm landing's review round piped grok's JSON through `tail -c` and lost
  findings 1–7; dispositions had to be reconstructed from the verdict
  line's own enumeration plus the visible tail. Reviewer output is
  evidence — evidence gets persisted before it gets summarized.
- 2026-07-14: Numbered citations into a sibling repo's forked ledgers
  (golden rules, testing patterns, runbook sections) must be re-derived
  per repo, never carried over — cite by name, or by number only after
  verifying it in that repo and marking it "this repo's numbering". The
  mm adaptation review caught the hub's "Golden Rule 11 (handle the
  error path)" pointing at mm's policy-cutover rule; theirs is 26.
- 2026-07-14: Guidance that changes process is never "low-risk additive" —
  it gets independent review before landing, like any behavior change.
  Same incident: cross-family review (Codex) caught citation-level defects
  (a misattributed escape hatch, a wrong section reference, a stale
  repository map) that two same-day architecture-level reviews missed —
  the different-family review rule earns its keep at the level of detail,
  not just the level of design.
- 2026-07-06: Large cohesive files are deliberate, not neglected debt — file
  size alone is never a split reason or a review finding. What binds instead
  are two floors: every implicit coupling gets an explicit marker or an
  enforcing helper at the edit point, and every state machine (live runtime
  coupling) gets a name and a contract test. Extraction is justified to create
  that testable boundary, not to shrink a file; splitting structurally coupled
  code manufactures false seams that breed parallel-implementation drift.
  Distilled as engineering-principles §14 (Cohesion Over File Size).
- 2026-07-02: Verification-lessons fold from the four-way backstitch
  implementation bake-off (four agents, same baseline, all passed automated
  gates, all diverged on everything unchecked — and each violated its own
  declared contract somewhere). Distilled here as Golden Rule 13,
  engineering-principles §12/§13 and the §8 reproduce-claims amendment,
  testing-patterns Patterns 5–6, the adversarial-acceptance-probes runbook,
  the decision-hierarchy baseline/deviation/claims additions, and the
  writing-plans deviation log. Full incident record: the backstitch repo's
  `docs/lessons.md`.
- 2026-04-07 (12 entries): bootstrap-era corrections, all since distilled
  into the operating model — [DOM-1], [DOM-3], [DOM-5]–[DOM-9], [DOM-11],
  [DOM-12], Golden Rules 7–8, and the writing-plans, hardening-plans,
  review-loops, maintaining-traceability, and skills-lifecycle runbooks.
  (distilled from 12 entries, 2026-04-07..2026-04-07, source 5927481)
