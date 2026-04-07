# Review, Skills, and Bootstrap Guidance Plan

Status: Completed 2026-04-07

## Goal

Extend the documentation operating model with independent review workflows,
agent bootstrap and availability recording, a reusable skills surface, and a
post-use improvement loop for skills and runbooks.

## Source Documents

Source specs:

- `docs/specs/01-development-documentation-operating-model.md` [DOM-1],
  [DOM-2], [DOM-3], [DOM-5], [DOM-8], [DOM-11], [DOM-12], [DOM-13]

Read first:

- `AGENTS.md`
- `docs/README.md`
- `docs/agent-context/README.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/maintaining-traceability.md`
- `docs/implementation/01-documentation-system.md`

## Context and Key Files

Files to modify:

- `README.md`
- `AGENTS.md`
- `CLAUDE.md`
- `docs/README.md`
- `docs/lessons.md`
- `docs/agent-context/README.md`
- `docs/agent-context/context.index.yaml`
- `docs/agent-context/principles.md`
- `docs/agent-context/engineering-principles.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/maintaining-traceability.md`
- `docs/specs/README.md`
- `docs/specs/01-development-documentation-operating-model.md`
- `docs/implementation/01-documentation-system.md`
- `docs/implementation/02-repository-map.md`

Files to add:

- `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md`
- `docs/agent-context/runbooks/skills-lifecycle.md`
- `docs/plans/2026-04-07-review-skills-bootstrap-plan.md`
- `docs/implementation/03-agent-inventory.md`
- `skills/README.md`
- `skills/_template/SKILL.md`

Style and guidance:

- `docs/agent-context/principles.md`
- `docs/agent-context/engineering-principles.md`
- `docs/specs/01-development-documentation-operating-model.md` [DOM-11],
  [DOM-12], [DOM-13]

Reuse:

- keep the review prompt direct and operational
- keep one canonical agent inventory note
- keep skills as a distinct surface from runbooks

## Invariants and Constraints

- Guidance must remain project-neutral and not depend on one person.
- Independent review must stay advisory but mandatory for non-trivial work.
- The authoring agent must explicitly answer review feedback.
- Skills must complement runbooks rather than duplicating them.
- Agent availability recording must stay lightweight and refreshable.

## Tasks

1. Update the governing spec and root guidance for review, skills, and
   bootstrap.
   - Outcome: repository-wide policy names the new workflow explicitly.
   - Files to touch:
     - `README.md`
     - `AGENTS.md`
     - `CLAUDE.md`
     - `docs/README.md`
     - `docs/specs/01-development-documentation-operating-model.md`
   - Read first:
     - the governing spec
     - the root guidance files
   - Update:
      - `README.md` to mention bootstrap, independent review, and `skills/`
      - `AGENTS.md` and `CLAUDE.md` to include review and skill expectations
      - `docs/README.md` to link the new runbooks and `skills/`
      - the spec to add review, skills, and bootstrap requirements
   - Tests:
     - inspect the touched files for consistent terminology and exact spec
       references
   - Done when:
     - the new workflow surfaces are visible from the repo entry points

2. Add reusable runbooks for review loops and skill lifecycle.
   - Outcome: a new contributor can follow the workflow without rediscovery.
   - Files to touch:
     - `docs/agent-context/README.md`
     - `docs/agent-context/context.index.yaml`
   - Files to add:
     - `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md`
     - `docs/agent-context/runbooks/skills-lifecycle.md`
   - Read first:
     - `docs/agent-context/runbooks/writing-plans.md`
     - `docs/agent-context/runbooks/maintaining-traceability.md`
   - Tests:
     - inspect the runbooks for direct, executable steps and explicit reviewer
       handoff behavior
   - Done when:
     - the workflow is documented in one canonical place

3. Update planning and traceability guidance to include review feedback loops
   and post-use improvement checks.
   - Outcome: plans and close-out behavior encode the new loop.
   - Files to touch:
     - `docs/agent-context/runbooks/writing-plans.md`
     - `docs/agent-context/runbooks/maintaining-traceability.md`
   - Read first:
     - the new runbooks
   - Tests:
     - inspect for explicit reviewer input, feedback handling, and improvement
       checks
   - Done when:
     - plan authors know how review findings are supposed to be handled

4. Create live scaffolding for skills and agent inventory.
   - Outcome: the repository is ready to record available agents and reusable
     workflow skills.
   - Files to add:
     - `docs/implementation/03-agent-inventory.md`
     - `skills/README.md`
     - `skills/_template/SKILL.md`
   - Files to touch:
     - `docs/implementation/01-documentation-system.md`
     - `docs/implementation/02-repository-map.md`
   - Tests:
     - inspect for clear ownership, current availability notes, and skill
       conventions
   - Done when:
     - the repo has a concrete place for agent inventory and skills

5. Run an independent review with a different agent and fold the feedback back
   into the docs.
   - Outcome: the workflow is demonstrated, not just described.
   - Files in scope:
     - all touched files in this plan
   - Read first:
     - the governing spec
     - this plan
     - the new runbooks
   - Tests:
     - collect reviewer findings and answer each one by changing docs or
       recording why no change is needed
   - Done when:
     - the completed work reflects the reviewer feedback loop

## Testing Plan

This is a docs-only change. Verification is by inspection and grep-based
document-quality gates rather than runtime behavior.

Checks:

- the spec names the new workflow surfaces
- the runbooks explain the reviewer handoff loop and skill promotion rule
- the repo contains a live skills directory and agent inventory note
- root docs point at the new surfaces

## Verification and Gates

Run:

```bash
rg -n "review|skill|bootstrap|agent inventory|different agent family" README.md AGENTS.md CLAUDE.md docs skills
find docs skills -type f | sort
rg -n " +$|\t+$|^<<<<<<<|^=======|^>>>>>>>" README.md AGENTS.md CLAUDE.md docs skills || true
```

Success looks like:

- the new workflow terms appear in the intended docs
- the new files exist in the tree
- the whitespace and merge-marker check prints no matches

## Independent Review Loop

Reviewer preference:

1. a different agent family than Codex
2. if several are available, one not already shaping the plan
3. if only same-family review is available, note that limitation

Reviewer inputs:

- `docs/specs/01-development-documentation-operating-model.md`
- this plan
- `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md`
- `docs/agent-context/runbooks/skills-lifecycle.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/maintaining-traceability.md`
- `docs/implementation/03-agent-inventory.md`
- root guidance and skills scaffold files touched by this plan

Review prompt:

> Read the plan at [path]. Carefully examine the plan and the associated code.
> Look for errors, bad ideas, and latent ambiguities. Don't do any
> implementation, but answer carefully: Could you implement this confidently and
> correctly if asked?

Feedback loop result:

- Gemini was present but blocked by missing credentials.
- Qwen was present but failed during invocation.
- Claude completed the independent review.
- Accepted findings:
  - add a standalone independent review section to this plan
  - define how agent availability is verified and recorded
  - tighten Task 1 so the per-file changes are explicit
  - strengthen the rule for reviewer confidence failures
  - add a formal governing spec section to the skill template
- Partially accepted findings:
  - clarify the runbook vs skill boundary with examples
- Rejected or no-change findings:
  - per-task verification remains inspection-based for this docs-only slice;
    that is consistent with [DOM-10], so no command-level expansion was added
  - the `Reuse` guidance remains in context sections because it names preferred
    local paths rather than hard invariants
  - no change to `docs/agent-context/lessons.md` was needed because it remains a
    stable pointer and the canonical lessons ledger already captured the new
    rules
- Follow-up review:
  - a second Claude review of the revised plan found no material structural
    findings

## Out of Scope

- automatic agent discovery tooling
- CI enforcement for review loops
- actual project-specific skills beyond the template scaffold

## Fresh-Eyes Review

Re-read the spec, this plan, and the new runbooks as if you were a new
engineer.

Check for:

- unclear distinction between runbooks and skills
- vague review instructions
- missing place to record available agents
- missing feedback loop from reviewer back to author

The review pass for this plan is only complete once an independent agent has
reviewed the new workflow docs and the results have been considered explicitly.
