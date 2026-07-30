# Documentation System

## Purpose and Scope

This document explains why the repository is organized around shared agent
context, specs, dated plans, implementation docs, reusable skills, independent
reviews, and a lessons ledger.

The current implementation surface is the documentation system itself. Product
code has not been added yet, so the repository's main architecture is the
documentation operating model.

Conceptual identity of that system (what agent-theory is for, progressive
theory disclosure, consumer replacement of program theory) lives in
`docs/program-theory.md`. This file remains realization rationale for the
doc layout, not a second program theory.

## Governing Spec References

- `docs/specs/01-development-documentation-operating-model.md` [DOM-2]
- `docs/specs/01-development-documentation-operating-model.md` [DOM-3]
- `docs/specs/01-development-documentation-operating-model.md` [DOM-4]
- `docs/specs/01-development-documentation-operating-model.md` [DOM-7]
- `docs/specs/01-development-documentation-operating-model.md` [DOM-8]

## Design Rationale

### Shared Agent Context

The repository keeps durable guidance in `docs/agent-context/` so multiple
agent tools can consume one source of truth. Root files such as `AGENTS.md` and
tool-specific aliases are intentionally thin entry points rather than separate
policy documents.

When the environment supports it, tool-specific root aliases should be symlinks
to `AGENTS.md` instead of copied content. This reduces drift. In this
repository, `CLAUDE.md` is such an alias.

### Independent Review as a First-Class Step

Agent authors are prone to blind spots, especially in plans. The repository
therefore treats independent review as part of the operating model rather than
optional polish. When available, a different agent family is preferred so the
review is less likely to mirror the original model's assumptions.

### Reusable Skills

Some recurring workflow knowledge is too detailed or task-shaped to live only
in broad runbooks. The `skills/` directory exists so repeated operational
knowledge such as running, testing, debugging, or release flows can become a
reusable instruction surface instead of remaining buried in lessons or plans.

### Bootstrap Scaffold

The repository also includes a small scaffold command in
`bin/bootstrap-agent-theory` so the neutral starter set can be installed into
another repository. The command is intentionally simple: it copies the reusable
starter corpus, generates a few repo-owned placeholder docs, and stops. It does
not attempt to merge with existing `AGENTS.md` files or infer repo-specific
engineering rules.

### Separate Specs, Plans, and Implementation Docs

The split exists because each document answers a different question:

- specs answer what should be true
- plans answer how a specific change will be executed without breaking
  load-bearing boundaries
- implementation docs answer why the current design exists and where it lives

Combining those roles makes documents harder to trust and easier to let drift.

### Documentation As a Delivery Gate

The repository treats documentation maintenance as part of completion because
the main failure mode in agentic development is silent drift between intent,
execution, and implementation.

## Boundaries and Invariants

- `docs/agent-context/` is the canonical shared context surface.
- `docs/specs/` is the source of truth for intended behavior.
- `docs/plans/` contains dated execution records.
- `docs/implementation/` explains rationale and edit points.
- `skills/` stores reusable task-scoped workflow instructions.
- `docs/lessons.md` is the one canonical lessons ledger.

These roles should stay distinct even as the repository grows.

## Key Files

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Primary agent entry point |
| `CLAUDE.md` | Symlink alias for Claude-style tooling |
| `bin/bootstrap-agent-theory` | Scaffold command for installing the neutral starter set into another repository |
| `docs/agent-context/README.md` | Shared context hub |
| `docs/specs/00-specs-index.md` | Numbered entry point for specs |
| `docs/specs/01-development-documentation-operating-model.md` | Governing operating-model spec |
| `docs/agent-context/runbooks/hardening-plans.md` | Required companion for risky or boundary-crossing implementation plans |
| `bin/check-dom15-fixtures` | Structural gate for the [DOM-15] classification fixture table (scaffolded) |
| `bin/check-doc-paths` | Path-claim integrity gate for guidance surfaces (scaffolded) |
| `bin/coalesce-check` | Coalescing state SHA/cue evidence trail (scaffolded) |
| `docs/plans/2026-04-07-development-documentation-foundation-plan.md` | Foundation plan modeling the workflow |
| `docs/plans/2026-04-07-review-skills-bootstrap-plan.md` | Plan adding review, skills, and bootstrap guidance |
| `docs/plans/2026-04-07-plan-hardening-guidance-plan.md` | Plan that hardened the repository's planning guidance |
| `docs/implementation/00-implementation-index.md` | Numbered entry point for implementation docs |
| `docs/implementation/02-repository-map.md` | Quick pointer map for important docs |
| `docs/implementation/03-agent-inventory.md` | Current observed agent availability and refresh guidance |
| `skills/README.md` | Skill directory conventions and promotion criteria |

## Change Guidance

When future work adds product code:

1. classify the task per [DOM-15] — planning artifacts and review scale
   with the class; the verification floor never does. The rationale:
   uniform heavyweight ceremony decays into performative compliance,
   which is high-variance; a right-sized mandatory floor gets genuine
   compliance. Classes 1–2 keep their record in the commit history
2. add or update the governing spec first
3. create a dated plan for classes 3 and above
3. for risky work, harden the plan before implementation by making invariants,
   hidden couplings, anti-mocking guidance, rollback or rollout, and one-way
   doors explicit
4. run independent plan review and feed the results back into the plan
5. add or update the relevant implementation note for the touched area
6. update the repository map when new entry points become important
7. decide whether repeated workflow knowledge should become or update a skill
8. capture reusable corrections in `docs/lessons.md`

## Related Plans

- `docs/plans/2026-04-07-development-documentation-foundation-plan.md`
- `docs/plans/2026-04-07-review-skills-bootstrap-plan.md`
- `docs/plans/2026-04-07-plan-hardening-guidance-plan.md`
