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
- 2026-04-07: Keep canonical agent guidance in shared repo-owned docs and make
  root agent files point to that context instead of carrying divergent copies.
- 2026-04-07: Non-trivial plans must be executable by a zero-context engineer:
  exact spec references, exact files, invariants, verification commands, and a
  fresh-eyes review are required.
- 2026-04-07: Specs define intended behavior; implementation docs explain why
  the current design exists. Blending those roles causes drift.
- 2026-04-07: Documentation maintenance is part of the completion gate. If code
  changes without plan/spec/implementation alignment, the work is incomplete.
- 2026-04-07: Non-trivial plans should be reviewed by an independent agent, and
  the authoring agent should answer each review point by updating the plan or
  documenting why the current path is still the best choice.
- 2026-04-07: When lessons cluster around a recurring workflow such as running,
  testing, debugging, or release work, promote that knowledge into a reusable
  skill in `skills/` instead of leaving it only in the lessons ledger.
- 2026-04-07: After using a skill or runbook, evaluate whether it should be
  improved while context is fresh.
- 2026-04-07: Prefer symlinks from tool-specific root guidance files such as
  `CLAUDE.md` to `AGENTS.md` when the environment supports them; thin pointer
  files are the fallback.
- 2026-04-07: Optimize docs for agent usability, not just human readability. If
  something is human-clear but agent-ambiguous, call it out and suggest a
  specific fix. Check for missing owner, boundary, verification, or required
  action.
- 2026-04-07: Plans usually fail at the boundaries, not the center. Over-specify
  invariants, hidden couplings, anti-mocking guidance, rollout/rollback, and
  one-way doors rather than letting implementers infer them.
- 2026-04-07: If rollback, rollout order, or post-deploy success cannot be
  described cleanly before implementation begins, the plan is still too loose
  for risky work.
- 2026-04-07: Required reading should not be a bare file list on risky work.
  Add enough current-structure context and comprehension questions that a
  zero-context implementer can find the right edit point before coding.
