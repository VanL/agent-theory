# Development Documentation Foundation Plan

Status: Completed 2026-04-07

## Goal

Establish a project-neutral, repo-owned documentation system for agentic
development in this repository, including shared agent context, specs, dated
plans, implementation docs, lessons learned, and explicit documentation
maintenance gates.

## Source Documents

Source specs:

- `docs/specs/00-development-documentation-operating-model.md` [DOM-1],
  [DOM-2], [DOM-3], [DOM-4], [DOM-5], [DOM-6], [DOM-7], [DOM-8], [DOM-9],
  [DOM-10]

Read first:

- `AGENTS.md`
- `docs/README.md`
- `docs/agent-context/README.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/writing-specs.md`
- `docs/agent-context/runbooks/writing-implementation-docs.md`
- `docs/agent-context/runbooks/maintaining-traceability.md`

## Context and Key Files

Files to modify:

- `README.md`
- `AGENTS.md`
- `CLAUDE.md`
- `docs/README.md`
- `docs/lessons.md`
- `docs/agent-context/README.md`
- `docs/agent-context/context.index.yaml`
- `docs/agent-context/decision-hierarchy.md`
- `docs/agent-context/principles.md`
- `docs/agent-context/engineering-principles.md`
- `docs/agent-context/lessons.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/writing-specs.md`
- `docs/agent-context/runbooks/writing-implementation-docs.md`
- `docs/agent-context/runbooks/testing-patterns.md`
- `docs/agent-context/runbooks/maintaining-traceability.md`
- `docs/specs/README.md`
- `docs/specs/00-development-documentation-operating-model.md`
- `docs/plans/README.md`
- `docs/plans/2026-04-07-development-documentation-foundation-plan.md`
- `docs/implementation/README.md`
- `docs/implementation/00-documentation-system.md`
- `docs/implementation/01-repository-map.md`

Style and guidance:

- `docs/specs/00-development-documentation-operating-model.md` [DOM-2],
  [DOM-4], [DOM-8]
- `docs/agent-context/principles.md`
- `docs/agent-context/engineering-principles.md`

Reuse:

- keep one canonical shared context in `docs/agent-context/`
- keep one canonical lessons ledger in `docs/lessons.md`
- model bidirectional spec/plan traceability in the starter documents

## Invariants and Constraints

- The repository guidance must stay project-neutral and not depend on a
  specific person, local environment, or sibling repository path.
- Plans must remain dated and executable by a zero-context engineer.
- Specs must remain the source of truth for intended behavior.
- Implementation docs must explain why, not become line-by-line narrations.
- Documentation maintenance must be framed as a delivery gate, not optional
  cleanup.
- The setup should stay small enough to use directly in a new repository.

## Tasks

1. Create root entry points and top-level documentation index.
   - Outcome: agents and humans have clear entry points into the shared context.
   - Files to touch:
     - `README.md`
     - `AGENTS.md`
     - `CLAUDE.md`
     - `docs/README.md`
   - Read first:
     - `docs/specs/00-development-documentation-operating-model.md` [DOM-1],
       [DOM-2], [DOM-3]
   - Reuse:
     - one canonical read order
   - Tests:
     - inspect the read order and directory descriptions for consistency
   - Done when:
     - root guidance points agents into `docs/agent-context/`

2. Create the shared agent-context hub and reusable runbooks.
   - Outcome: the repository has durable, reusable guidance for planning,
     specs, implementation docs, testing, and traceability.
   - Files to touch:
     - `docs/agent-context/*`
   - Read first:
     - `docs/specs/00-development-documentation-operating-model.md` [DOM-3],
       [DOM-4], [DOM-5], [DOM-6], [DOM-7], [DOM-8]
   - Reuse:
     - one canonical context index
     - one canonical lessons pointer
   - Tests:
     - inspect runbooks for direct, operational wording
   - Done when:
     - a zero-context engineer can discover how this repo expects work to be
       done

3. Create starter specs, plans, and implementation docs that model the system.
   - Outcome: the repository demonstrates its own workflow with live examples.
   - Files to touch:
     - `docs/specs/*`
     - `docs/plans/*`
     - `docs/implementation/*`
   - Read first:
     - `docs/specs/00-development-documentation-operating-model.md`
     - `docs/agent-context/runbooks/writing-plans.md`
     - `docs/agent-context/runbooks/writing-specs.md`
     - `docs/agent-context/runbooks/writing-implementation-docs.md`
   - Reuse:
     - exact spec references
     - plan backlink pattern
     - implementation rationale pattern
   - Tests:
     - inspect backlink integrity and directory role separation
   - Done when:
     - the repo contains a starter spec, a dated plan, and implementation notes
       that refer to each other correctly

4. Seed the canonical lessons ledger and repository map.
   - Outcome: reusable lessons and an orientation map exist from day one.
   - Files to touch:
     - `docs/lessons.md`
     - `docs/implementation/01-repository-map.md`
   - Read first:
     - `docs/specs/00-development-documentation-operating-model.md` [DOM-2],
       [DOM-9]
   - Constraints:
     - keep lessons short and reusable
   - Tests:
     - inspect lesson format and map usefulness
   - Done when:
     - a new contributor can find the important docs quickly

5. Perform a fresh-eyes review on the full documentation system.
   - Outcome: the initial setup is internally consistent and directly usable.
   - Files to touch:
     - all files created in this plan
   - Read first:
     - entire plan
     - entire starter spec
   - Tests:
     - review for missing backlinks, duplicated guidance, me-specific wording,
       or vague task instructions
   - Done when:
     - the repository reads like a reusable starter kit rather than a personal
       notes dump

## Testing Plan

This is a docs-only change. Verification is by inspection and document-quality
gates rather than runtime behavior.

Checks:

- exact spec references are present in the plan
- the spec contains a `## Related Plans` backlink
- the implementation docs explain rationale, not only structure
- the runbooks cover planning, specs, implementation docs, testing, and
  traceability
- the language stays project-neutral

## Verification and Gates

Run:

```bash
rg -n " +$|\t+$|^<<<<<<<|^=======|^>>>>>>>" README.md AGENTS.md CLAUDE.md docs || true
rg -n "Related Plans|Fresh-Eyes Review|Documentation maintenance|why the current design exists|zero-context engineer" docs AGENTS.md README.md CLAUDE.md
find docs -type f | sort
```

Success looks like:

- the whitespace and merge-marker check prints no matches
- the expected guidance terms appear in the right files
- the docs tree contains the planned scaffold

## Out of Scope

- product code, tests, or runtime configuration for an actual application
- agent-vendor-specific prompt engineering beyond neutral entry points
- CI automation for enforcing these docs

## Fresh-Eyes Review

Re-read the starter spec, this plan, and the implementation notes as if you are
a new engineer with no prior context.

Check for:

- missing file paths
- duplicated source-of-truth claims
- vague statements about plans, specs, or implementation docs
- personal or local-environment assumptions
- missing completion gates

The review pass for this plan was satisfied by ensuring the repository-local
docs explain the operating model without referring back to user-specific paths
or private workflow knowledge.
