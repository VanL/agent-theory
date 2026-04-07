# Repository Map

Quick pointers to the key documents in this repository.

## Root Entry Points

| Path | Purpose |
|------|---------|
| `README.md` | Top-level overview |
| `AGENTS.md` | Canonical agent entry point |
| `CLAUDE.md` | Symlink alias for Claude-style tooling |

## Shared Agent Context

| Path | Purpose |
|------|---------|
| `docs/agent-context/README.md` | Context hub and read order |
| `docs/agent-context/context.index.yaml` | Machine-readable context index |
| `docs/agent-context/decision-hierarchy.md` | Conflict-resolution order |
| `docs/agent-context/principles.md` | Shared execution principles |
| `docs/agent-context/engineering-principles.md` | Engineering rules and warning signs |

## Runbooks

| Path | Purpose |
|------|---------|
| `docs/agent-context/runbooks/writing-plans.md` | Plan-writing standard |
| `docs/agent-context/runbooks/hardening-plans.md` | Required hardening checklist for risky or boundary-crossing plans |
| `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md` | Independent review workflow and agent bootstrap |
| `docs/agent-context/runbooks/writing-specs.md` | Spec-writing standard |
| `docs/agent-context/runbooks/writing-implementation-docs.md` | Implementation-doc standard |
| `docs/agent-context/runbooks/testing-patterns.md` | Testing and verification guidance |
| `docs/agent-context/runbooks/maintaining-traceability.md` | Documentation-maintenance gate |
| `docs/agent-context/runbooks/skills-lifecycle.md` | Skill promotion and maintenance guidance |

## Core Documentation Corpus

| Path | Purpose |
|------|---------|
| `docs/specs/00-development-documentation-operating-model.md` | Governing spec for this repository's doc workflow |
| `docs/plans/2026-04-07-development-documentation-foundation-plan.md` | Foundation plan that created the scaffold |
| `docs/plans/2026-04-07-review-skills-bootstrap-plan.md` | Plan that added review loops, skills, and bootstrap guidance |
| `docs/plans/2026-04-07-plan-hardening-guidance-plan.md` | Plan that strengthened the planning quality bar |
| `docs/implementation/00-documentation-system.md` | Why the documentation system is shaped this way |
| `docs/implementation/02-agent-inventory.md` | Current observed agent availability and review preference |
| `docs/lessons.md` | Canonical lessons ledger |

## Skills

| Path | Purpose |
|------|---------|
| `skills/README.md` | Skill directory purpose and conventions |
| `skills/_template/SKILL.md` | Starter template for new reusable skills |

## Update Guidance

When the repository grows:

- add new important entry points here
- keep descriptions short and navigational
- prefer linking to the document that explains a concept, not every file that
  happens to mention it
