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
