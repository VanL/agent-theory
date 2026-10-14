# Documentation System

## Purpose and Scope

This document explains why the repository separates shared agent context,
program theory, behavioral specs, dated execution plans, implementation notes,
reusable skills, independent reviews, and lessons learned into distinct files.

In the Agent Theory hub, the documentation and verification scripts *are* the
system. The conceptual identity of Agent Theory lives in
`docs/program-theory.md`; this file explains the practical layout of the
documentation directories.

## Governing Spec References

- `docs/specs/01-development-documentation-operating-model.md` `[DOM-2]`
- `docs/specs/01-development-documentation-operating-model.md` `[DOM-3]`
- `docs/specs/01-development-documentation-operating-model.md` `[DOM-4]`
- `docs/specs/01-development-documentation-operating-model.md` `[DOM-7]`
- `docs/specs/01-development-documentation-operating-model.md` `[DOM-8]`

## Design Rationale

### One Shared Agent Context (`docs/agent-context/`)

Keeping durable rules and runbooks in `docs/agent-context/` lets every coding
agent (`claude`, `codex`, `gemini`, and IDE harnesses) read one source of
truth. Root files such as `AGENTS.md` and `CLAUDE.md` stay thin entry points
rather than separate, drifting policy documents. Where the filesystem supports
symlinks, `CLAUDE.md` symlinks directly to `AGENTS.md`.

### Independent Review as a Built-In Step

An agent that writes a plan or patch tends to share its own framing blind
spots. Treating independent review (`[DOM-11]`) as a required step—run by a
different model family via `skills/call-agent/SKILL.md`, with same-family
fallback permitted only after recorded Tier-1 unavailability—catches false
premises and weak tests before changes land.

### Reusable Skills (`skills/`)

Step-by-step procedures for recurring tasks—such as running an independent
review, crystallizing a program theory, debugging a failure, or coalescing old
plans—are too detailed to load on every session start. Storing them in
`skills/` keeps session startup lean while giving agents an explicit playbook
when those tasks arise.

### Safe Bootstrap Installer (`bin/bootstrap-agent-theory`)

`bin/bootstrap-agent-theory` installs the starter files and verification gates
into a target repository. By default it only creates missing files: it never
overwrites an existing `AGENTS.md` without `--force` and never invents product
architecture.

### Why Theory, Specs, Plans, and Implementation Docs Stay Separate

Combining every kind of documentation into one file makes it hard to tell what
is a current requirement versus an old plan or an aspirational idea. Here, each
surface answers one question:

- **Program theory** (`docs/program-theory.md`) answers *what kind of system
  this is and what it refuses to do*.
- **Specs** (`docs/specs/`) answer *what exact behavior must hold right now*.
- **Plans** (`docs/plans/`) answer *how a specific change is being executed and
  verified*.
- **Implementation docs** (`docs/implementation/`) answer *why the code is
  structured this way and where to edit it*.

### Documentation as a Completion Gate

The most common failure mode in agent-assisted development is silent drift
between what the docs say and what the code actually does. Treating
documentation updates and path/fixture gate checks as part of the completion
gate prevents that drift from accumulating.

## Boundaries and Invariants

- `docs/program-theory.md` holds the repository's conceptual model and
  non-goals.
- `docs/agent-context/` is the canonical shared context and runbook directory.
- `docs/specs/` is the source of truth for intended behavior.
- `docs/plans/` holds dated execution plans and the plan status index.
- `docs/implementation/` explains design rationale, boundaries, and key edit
  points.
- `skills/` stores reusable task-specific workflows.
- `docs/lessons.md` is the single lessons ledger, paired with
  `docs/coalescing.md`.

## Key Files

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Primary agent entry point |
| `CLAUDE.md` | Symlink alias for Claude-style tooling |
| `bin/bootstrap-agent-theory` | Installer that copies the starter scaffold into another repository |
| `docs/agent-context/README.md` | Shared context overview and read order |
| `docs/specs/00-specs-index.md` | Numbered entry point for specs |
| `docs/specs/01-development-documentation-operating-model.md` | Governing operating-model spec (`[DOM-*]`) |
| `docs/agent-context/runbooks/hardening-plans.md` | Required checklist for risky or boundary-crossing plans |
| `bin/check-dom15-fixtures` | Gate verifying the `[DOM-15]` classification fixture table |
| `bin/check-doc-paths` | Gate verifying that backticked `docs/`, `skills/`, and `bin/` paths exist |
| `bin/coalesce-check` | Gate verifying commit SHAs and retrieval cues in `docs/coalescing.md` |
| `docs/plans/2026-04-07-development-documentation-foundation-plan.md` | Foundation plan modeling the workflow |
| `docs/plans/2026-04-07-review-skills-bootstrap-plan.md` | Plan adding review, skills, and bootstrap guidance |
| `docs/plans/2026-04-07-plan-hardening-guidance-plan.md` | Plan that hardened the planning guidance |
| `docs/implementation/00-implementation-index.md` | Numbered entry point for implementation docs |
| `docs/implementation/02-repository-map.md` | Quick pointer map for key repository files |
| `docs/implementation/03-agent-inventory.md` | Observed agent CLI availability and review preferences |
| `skills/README.md` | Skill directory conventions and promotion criteria |

## Change Guidance

When making changes in an Agent Theory repository:

1. **Classify the task per `[DOM-15]`.** Planning ceremony scales with the task
   class (`0–5`), while verification standards stay strict across all classes.
   Small changes (Classes `1–2`) record their rationale in the commit message;
   Classes `3–5` use a dated plan in `docs/plans/`.
2. **Update the governing spec first** (or alongside the code) whenever
   intended behavior changes.
3. **Write a dated plan** in `docs/plans/` and register it in
   `docs/plans/README.md` for Class `3+` work.
4. **Harden risky plans before coding** using
   `docs/agent-context/runbooks/hardening-plans.md` (invariants, hidden
   couplings, anti-mocking rules, rollback/rollout order, and one-way doors).
5. **Run an independent review** (`skills/call-agent/SKILL.md`) on the plan and
   the finished change, and address every finding.
6. **Update implementation docs and `docs/implementation/02-repository-map.md`**
   when design rationale, ownership, or entry points change.
7. **Promote recurring workflows into `skills/`** and record reusable
   corrections in `docs/lessons.md`.

## Related Plans

- `docs/plans/2026-04-07-development-documentation-foundation-plan.md`
- `docs/plans/2026-04-07-review-skills-bootstrap-plan.md`
- `docs/plans/2026-04-07-plan-hardening-guidance-plan.md`
