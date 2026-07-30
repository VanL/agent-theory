# Agent-Theory

**Human entry** for the project-neutral guidance system used when coding agents
are first-class collaborators. For the conceptual account agents should load
first in *this* repository, see
[`docs/program-theory.md`](docs/program-theory.md).

## What this is

Agent-theory is a **repo-owned operating model and theory-transfer kit** for
agentic software development. It is not an application framework and not a
product runtime. It helps a repository keep a **shared language**—concepts,
boundaries, ownership, non-goals, and why the system has its shape—while
humans and agents change the code.

The intellectual spine (expanded in the program theory):

- **Peter Naur** — programming as *theory building*; documentation is
  secondary to possession of the working model.
- **Donald Knuth** — explanation addressed to understanding, kept in contact
  with realization (here: separate surfaces linked by traceability, not one
  master literate file).
- **Armin Ronacher** — under AI assistance the tower can keep rising after
  shared architectural language has already collapsed; deliberate orientation
  and friction are responses, not nostalgia.

## What problem it addresses

Agents are strong at local coherence and weak at global product identity
unless that identity is externalized and loaded at the right scope. Process
alone is not enough; neither is a giant README. Agent-theory packages:

| Piece | Role |
|-------|------|
| Shared agent context | Session entry, principles, runbooks |
| Operating-model spec | Normative process (`[DOM-*]`) |
| Program theory | Conceptual identity (hub vs **product-specific** in consumers) |
| Plans / reviews / lessons | Execution, independent check, durable corrections |
| Skills | Recurring workflows (including crystallizing product theory) |
| Bootstrap + gates | Install the neutral surface; check fixtures and path claims |

## Install into another repository

```bash
./bin/bootstrap-agent-theory /path/to/target-repo
```

- **Create-only by default.** Use `--dry-run` to inspect; `--force` only when
  you intend to overwrite scaffold files.
- **Non-magical:** no merge of conflicting constitutions; no invention of
  product architecture.
- After install, **replace** the product `docs/program-theory.md` stub with
  your product's theory. Use
  `skills/crystallize-program-theory/SKILL.md` (interview-style) rather than
  keeping the hub's theory of agent-theory as product identity.

Scaffolded gates (installed by default):

- `bin/check-dom15-fixtures` — [DOM-15] fixture table
- `bin/check-doc-paths` — backticked path claims must resolve
- `bin/coalesce-check` — coalescing SHA/cue evidence trail

## Humans vs agents

| Audience | Start here |
|----------|------------|
| **Humans** | This README → `docs/README.md` → operating-model spec as needed |
| **Agents (this hub)** | `AGENTS.md` → **`docs/program-theory.md`** → `docs/agent-context/` read order |
| **Agents (product repo after bootstrap)** | That repo's `AGENTS.md` → **its** `docs/program-theory.md` (product) → agent-context |

Product repositories should not leave the hub's conceptual account in place
as if it described their application.

**Extending the model:** keep product `docs/program-theory.md` short. When a
subsystem needs its own generative rule, ownership table, or non-goals, write
**module theory** next to that code (typical name `MODULE-THEORY.md`). That is
the normal way to deepen theory under agentic work—not stuffing the product
file, and not leaving local identity only in chat. See
[`docs/program-theory.md`](docs/program-theory.md) [AT-THEORY-2.1].

## Operating model (short)

- Shared agent context loads at session start.
- Specs define intended **behavior**; program theory defines conceptual
  **identity**; plans define in-flight **execution**; implementation docs
  explain **why** the realization looks as it does.
- Independent review for non-trivial plans and material completions.
- Documentation maintenance is part of done, not cleanup.
- Coalescing folds lessons/plans/skills sediment under thresholds.

Detail: `docs/specs/01-development-documentation-operating-model.md`.

## Start here (humans)

1. This README.
2. [`docs/program-theory.md`](docs/program-theory.md) — what agent-theory *is*
   (optional for a quick tour; required before changing hub identity).
3. [`docs/README.md`](docs/README.md) — doc map by task.
4. [`docs/specs/01-development-documentation-operating-model.md`](docs/specs/01-development-documentation-operating-model.md).
5. [`docs/implementation/00-implementation-index.md`](docs/implementation/00-implementation-index.md).

## Layout

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Agent entry (permissions, conventions, read order) |
| `CLAUDE.md` | Symlink alias → `AGENTS.md` |
| `docs/program-theory.md` | **Hub** program theory (replace in product repos) |
| `docs/agent-context/` | Shared context and runbooks |
| `docs/specs/` | Process (and any future hub) contracts |
| `docs/plans/` | Dated execution plans |
| `docs/implementation/` | Rationale and maps for this system |
| `skills/` | Task-scoped workflows |
| `bin/bootstrap-agent-theory` | Scaffold installer |
| `docs/lessons.md` | Lessons ledger |
| `docs/coalescing.md` | Coalescing state |

## Crystallizing product or module theory

In a product repository:

```text
skills/crystallize-program-theory/SKILL.md
```

Interview the owner one decision at a time. Outcomes:

- **Product theory** — replace `docs/program-theory.md` (apex shared language).
- **Module theory** — extend the model at the module root when depth is local
  ([AT-THEORY-2.1]); wire entry so agents load it **on entry to that module**,
  not on every session start.

Both are the same skill and spine; the scope (product vs module) is an explicit
decision in the interview.

## Current state

This repository is the **guidance system** (and its own dogfood). It does not
ship application product code. Consumer dogfood drives revisions; this is a
first full externalization of the hub's program theory (2026-07-30 draft).

## Related

- [agent-mcp](https://github.com/VanL/agent-mcp) — MCP tooling and related
  agent-facing infrastructure
