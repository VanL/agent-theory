# Project-Neutral Agentic Development Guidance

This repository is set up as a reusable, repo-owned documentation system for
agentic software development.

It also includes a scaffold command for installing the neutral starter set into
another repository without trying to merge or infer repo-specific guidance:

```bash
./bin/bootstrap-agent-theory /path/to/target-repo
```

The bootstrap is create-only by default. Use `--dry-run` to inspect actions and
`--force` only when you want to overwrite existing scaffold files deliberately.
It is intentionally non-transactional and intentionally non-magical: if a run
fails or if you are updating an existing install, inspect the target and diff
before re-running with `--force`. The target repo still needs human adaptation,
especially in `AGENTS.md`, `docs/README.md`,
`docs/agent-context/engineering-principles.md`, and the implementation-doc
placeholders.

Scaffolded guidance gates (also installed into consumers by default):

- `bin/check-dom15-fixtures` — structural gate for the [DOM-15] fixture table
- `bin/check-doc-paths` — every backticked docs/skills/bin path claim must resolve
- `bin/coalesce-check` — coalescing state SHA/cue evidence trail

The operating model is:

- shared agent context is loaded at session start
- available agent tools are discovered and recorded at bootstrap
- specs in `docs/specs/` define intended behavior
- dated plans in `docs/plans/` define execution, and risky plans are hardened
  against boundary regressions before implementation starts
- independent review agents review plans and completed work
- implementation docs in `docs/implementation/` explain why the code is shaped
  the way it is
- reusable workflow instructions can be promoted into `skills/`
- durable corrections land in `docs/lessons.md`
- documentation maintenance is part of the completion gate, not cleanup

## Start Here

1. Read `AGENTS.md`.
2. Read `docs/agent-context/README.md`.
3. Read `docs/specs/00-specs-index.md`.
4. Read `docs/specs/01-development-documentation-operating-model.md`.
5. Read `docs/implementation/00-implementation-index.md`.

## Layout

- `AGENTS.md`: canonical repo entry point for agents
- `CLAUDE.md`: symlink alias for tools that load Claude-style root guidance
- `docs/agent-context/`: shared context and reusable runbooks
- `docs/specs/`: intended behavior and invariants
- `docs/plans/`: dated implementation plans
- `docs/implementation/`: current architecture rationale and repository map
- `skills/`: reusable task-scoped instructions and workflow assets
- `docs/lessons.md`: canonical lessons ledger

## Current State

This repository currently contains the guidance system itself. As product code
is added, keep the same traceability loop intact:

`spec section <-> plan <-> implementation doc <-> code`

## Related Projects

- [agent-mcp](https://github.com/VanL/agent-mcp): MCP tooling and related
  agent-facing infrastructure
