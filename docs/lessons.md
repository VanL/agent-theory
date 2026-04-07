# Lessons Learned

Use this file for durable, project-level lessons that should influence future
sessions.

## When To Add A Lesson

- A correction exposed a repeated failure mode.
- A missing document or runbook caused rework.
- A plan or spec was too ambiguous to execute safely.
- A completed change revealed a stronger general rule than the repo previously
  encoded.

## Lessons

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
