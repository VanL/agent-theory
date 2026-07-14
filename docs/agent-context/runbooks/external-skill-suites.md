# External Skill Suites: Compatibility and Precedence

Many environments ship skill suites that agents pick up naturally —
superpowers, gstack, Every's compound-engineering plugin, and similar.
These suites converge on the same disciplines this repository encodes
(zero-context plans, evidence before claims, root-cause-first debugging,
independent review). Use them; do not fight them. This runbook declares
how they compose with repo guidance.

Owner: the agent invoking an external skill. Boundary: applies whenever an
external skill fires on work governed by a repo doc; it does not restrict
skills on work the repo does not govern. Verification: when an external
skill's output conflicts with a repo doc, the repo doc's gate decides.
Required action: follow the external skill's *process* and this repo's
*contract* — locations, formats, invariants, and completion gates come
from the repo docs mapped below.

## Precedence

Repository guidance governs when an external skill and a repo doc
conflict. This is not a power grab: superpowers' own priority rules place
user and repository instructions (CLAUDE.md / AGENTS.md) above its skills.
The decision hierarchy in `../decision-hierarchy.md` applies unchanged;
external skills sit with "agent inference" — useful momentum, lowest
tier when in conflict.

## Crosswalk

| External skill | Governing repo doc | Note |
|---|---|---|
| superpowers:brainstorming | [DOM-5]; `writing-plans.md` | Exploration precedes planning; output feeds a dated plan in `docs/plans/`, never replaces one |
| superpowers:writing-plans | `writing-plans.md` | Highly convergent. Repo governs plan shape and location (`docs/plans/YYYY-MM-DD-*.md`, not `docs/superpowers/plans/`) |
| superpowers:executing-plans, subagent-driven-development, dispatching-parallel-agents | `AGENTS.md` subagent contract | The delegation contract (verify and integrate before returning; no re-delegation) is not waivable |
| superpowers:test-driven-development | `engineering-principles.md` §10 | Same rule, but §10's escape hatch governs: when a failing test is impractical, name the replacement proof — do not skip, do not fake |
| superpowers:verification-before-completion | [DOM-10]; `../decision-hierarchy.md` completion gate | Same iron law: a status document is a claim; evidence is a rerun |
| superpowers:requesting-code-review, receiving-code-review | `review-loops-and-agent-bootstrap.md`; [DOM-11] | Reproduce findings before acting (§8); record dispositions in the plan |
| superpowers:systematic-debugging | `skills/debugging/SKILL.md` | Repo-owned distillation; either works — the repo skill adds the repo's proof and replan gates |
| superpowers:using-git-worktrees | dirty-tree discipline (`../principles.md`) | Compatible as-is |
| superpowers:finishing-a-development-branch | Definition of Done in `AGENTS.md` | Includes the no-AI-attribution rule for commits and PRs |
| superpowers:writing-skills | `skills-lifecycle.md` | Repo skills follow `skills/_template/SKILL.md`, not the superpowers format |
| gstack plan-eng-review, plan-ceo-review, grilling, review | `review-loops-and-agent-bootstrap.md` | Acceptable reviewer personas for the independent review loop; dispositions still land in the plan |
| gstack spec | `writing-specs.md` | Repo governs spec shape: stable reference codes, `## Related Plans`, verification expectations |

## Known Conflicts (repo wins; know why)

- **File size.** superpowers:writing-plans prefers "smaller, focused
  files." This repo's `engineering-principles.md` §14 (cohesion over file
  size) governs: no split on size grounds alone; the two floors (coupling
  markers, named state machines) decide.
- **Plan location and header format.** Plans live in `docs/plans/` with
  the repo's required sections — not the external suite's default path or
  header.
- **TDD absolutism.** "No failing test means you don't understand the
  bug" is pressure, not physics. §10's escape hatch (name the replacement
  proof) governs docs-only changes, nondeterministic races, and
  infrastructure failures.

## Every's Compound Engineering

The compound-engineering plugin's loop (Plan → Work → Review → Compound)
maps directly onto this operating model: Plan ≈ [DOM-5], Review ≈
[DOM-11], Compound ≈ [DOM-9] lessons plus the [DOM-14] coalescing layer —
their `/workflows:compound` step is this repo's coalescing sweep in its
additive phase, and their `docs/solutions/` is this repo's lessons ledger.
Its review agents are acceptable reviewer personas under [DOM-11]. The
same precedence applies: their plan documents feed `docs/plans/`; the
repo's spec layer (which the plugin does not have) remains the source of
truth above plans.

## Maintenance

- Crosswalk rows are claims: when an external skill fires and this table
  misleads, fix the row and note it in `docs/lessons.md`.
- External-skill firings are promotion-tier citation evidence under
  [DOM-14]: if sessions repeatedly lean on an external skill with no repo
  equivalent, that is the signal to harvest a repo-owned version.
- External suites version faster than this repo syncs. Never vendor them;
  cite them.
