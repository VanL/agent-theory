# Repository Map

Quick pointers to the key documents in this repository.

## Root Entry Points

| Path | Purpose |
|------|---------|
| `README.md` | Top-level overview |
| `AGENTS.md` | Canonical agent entry point |
| `CLAUDE.md` | Symlink alias for Claude-style tooling |
| `bin/bootstrap-agent-theory` | Scaffold command for installing the neutral starter set into another repository (adapts hub plan citations to foreign-name form at copy time; copies the three guidance gates below) |
| `bin/check-doc-paths` | Gate: every backticked repo-relative path claim in the guidance surfaces resolves — tree and `--scaffold` modes (scaffolded to consumers) |
| `bin/coalesce-check` | Evidence trail for the coalescing layer: derives counts, verifies every run-log SHA/cue (local, sibling, and published-remote), reports local-only pins (scaffolded to consumers) |
| `bin/check-dom15-fixtures` | Structural gate for the [DOM-15] classification fixture table (scaffolded to consumers) |

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
| `docs/agent-context/runbooks/designing-agent-facing-interfaces.md` | Principles for designing APIs, CLIs, and docs that agents consume (first [DOM-14] fold-up, from mm) |

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
| `skills/interface-review/SKILL.md` | Review an agent-facing surface (REST/MCP/CLI/doc) against `designing-agent-facing-interfaces.md` |

## Update Guidance

When the repository grows:

- add new important entry points here
- keep descriptions short and navigational
- prefer linking to the document that explains a concept, not every file that
  happens to mention it
