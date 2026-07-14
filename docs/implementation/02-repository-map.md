# Repository Map

Quick pointers to the key documents in this repository.

## Root Entry Points

| Path | Purpose |
|------|---------|
| `README.md` | Top-level overview |
| `AGENTS.md` | Canonical agent entry point |
| `CLAUDE.md` | Symlink alias for Claude-style tooling |
| `bin/bootstrap-agent-guidance` | Scaffold command for installing the neutral starter set into another repository |

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
| `docs/agent-context/runbooks/adversarial-acceptance-probes.md` | Black-box invariant floors for agent-built tools |
| `docs/agent-context/runbooks/external-skill-suites.md` | Precedence and crosswalk for external skill suites |

## Core Documentation Corpus

| Path | Purpose |
|------|---------|
| `docs/specs/00-specs-index.md` | Numbered entry point for specs |
| `docs/specs/01-development-documentation-operating-model.md` | Governing spec for this repository's doc workflow |
| `docs/plans/2026-04-07-development-documentation-foundation-plan.md` | Foundation plan that created the scaffold |
| `docs/plans/2026-04-07-review-skills-bootstrap-plan.md` | Plan that added review loops, skills, and bootstrap guidance |
| `docs/plans/2026-04-07-plan-hardening-guidance-plan.md` | Plan that strengthened the planning quality bar |
| `docs/implementation/00-implementation-index.md` | Numbered entry point for implementation docs |
| `docs/implementation/01-documentation-system.md` | Why the documentation system is shaped this way |
| `docs/implementation/03-agent-inventory.md` | Current observed agent availability and review preference |
| `docs/lessons.md` | Canonical lessons ledger |
| `docs/coalescing.md` | Coalescing state per [DOM-14]: thresholds, watermarks, deferrals, run log |

## Skills

| Path | Purpose |
|------|---------|
| `skills/README.md` | Skill directory purpose and conventions |
| `skills/_template/SKILL.md` | Starter template for new reusable skills |
| `skills/coalescing/SKILL.md` | Coalescing sweep per [DOM-14] |
| `skills/debugging/SKILL.md` | Root-cause-first debugging |
| `skills/brainstorming-to-plan/SKILL.md` | Bridge from exploration to plan or spec delta |
| `skills/call-agent/SKILL.md` | Invoke an independent reviewer agent (read-only postures, probes) |
| `skills/propagate-guidance/SKILL.md` | Hub-native: land a guidance wave in a sibling repo (not scaffolded) |

## Update Guidance

When the repository grows:

- add new important entry points here
- keep descriptions short and navigational
- prefer linking to the document that explains a concept, not every file that
  happens to mention it
