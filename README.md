# Agent Theory

**Delegate implementation, not understanding.**

Agent Theory is a practical discipline for building software with coding
agents while keeping humans in possession of the program's theory: what the
system is, why it has its shape, what it does not do, and how change is proved.

It is not big design up front. The theory begins partial and is refined
feature by feature through dialogue, specifications, implementation, review,
and evidence.

This repository is the **reference operating model and starter corpus** for
applying that discipline inside a codebase. The repository slug and command
path are `agent-theory`; the human brand is **Agent Theory** (no hyphen).

## The failure mode

Coding agents can decouple software construction from human understanding. A
codebase may continue growing while neither the human nor the agents share a
coherent account of the whole. Agent Theory treats human understanding as a
deliverable of agent-assisted development—not a private side effect that
might or might not survive the next refactor.

That stance follows a short intellectual lineage:

- **Peter Naur** — programming as *theory building*; documentation is secondary
  to possession of the working model.
- **Donald Knuth** — explanation addressed to understanding, kept in contact
  with realization (here: separate surfaces linked by traceability, not one
  master literate file).
- **Armin Ronacher** — under AI assistance the tower can keep rising after
  shared architectural language has already collapsed; deliberate orientation
  and friction are responses, not nostalgia.

Primer (what the terms mean):
[`docs/specs/02-agent-theory-and-program-theory.md`](docs/specs/02-agent-theory-and-program-theory.md).  
This repository's identity account:
[`docs/program-theory.md`](docs/program-theory.md).

## What the corpus provides

| Piece | Role |
|-------|------|
| Shared agent context | Session entry, principles, runbooks |
| Operating-model spec | Normative process (`[DOM-*]`) |
| Program theory | Conceptual identity of **this repository** (product-specific after bootstrap) |
| Plans / reviews / lessons | Execution, independent check, durable corrections |
| Skills | Recurring workflows (including crystallizing product theory) |
| Bootstrap + gates | Install the neutral surface; check fixtures and path claims |

Artifact roles stay separate: theory answers *what kind of system this is*;
contracts answer *what exact behavior is intended*; implementation docs answer
*why the realization looks like this*; process keeps those surfaces honest
under agent labor.

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
  `skills/crystallize-program-theory/SKILL.md` (interview-style). Exploration
  may proceed while the file is a stub; do not commit product-scope behavior
  or architecture treating the stub (or hub meta-theory) as product authority.
  Product-scope Class 5 work needs at least a current Draft account, revised
  as implementation exposes new facts.

Scaffolded gates (installed by default):

- `bin/check-dom15-fixtures` — [DOM-15] fixture table
- `bin/check-doc-paths` — backticked path claims must resolve
- `bin/coalesce-check` — coalescing SHA/cue evidence trail

## Humans vs agents

| Audience | Start here |
|----------|------------|
| **Humans** | This README → `docs/README.md` → operating-model spec as needed |
| **Agents** | `AGENTS.md` → **`docs/program-theory.md`** (this repo's theory) → agent-context read order |

**Extending the model:** keep product `docs/program-theory.md` short. When a
subsystem needs its own generative rule, ownership table, or non-goals, write
**module theory** next to that code (typical name `MODULE-THEORY.md`). Load it
on entry to that module, not on every session start. See
[`docs/program-theory.md`](docs/program-theory.md) [AT-THEORY-2.1] and the
crystallize skill for the drafting checklist.

## Operating model (short)

- Shared agent context loads at session start; program theory first among
  conceptual surfaces ([DOM-2], [DOM-3]).
- Specs define intended **behavior**; program theory defines conceptual
  **identity**; plans define in-flight **execution**; implementation docs
  explain **why** the realization looks as it does.
- Independent review for non-trivial plans and material completions.
- Documentation maintenance is part of done, not cleanup.
- Coalescing folds lessons/plans/skills sediment under thresholds.
- Normative guidance is trusted from the **base revision**; task-branch
  guidance edits are review material until approved (see decision hierarchy).

Detail: `docs/specs/01-development-documentation-operating-model.md`.

## Provenance and dogfood

The practices in this repository developed through sustained agent-assisted
work on [SimpleBroker](https://github.com/VanL/simplebroker) and a larger
private system. They were extracted into Agent Theory and then used from the
beginning in [Taut](https://github.com/VanL/taut) and
[Backstitch](https://github.com/VanL/backstitch), while being grafted back into
SimpleBroker, [Weft](https://github.com/VanL/weft), and other repositories.

That is factual provenance and adoption, not a claim that the framework caused
a measured improvement. Comparative efficacy arguments belong in external
writing that cites this corpus. Case studies, when written, should be linked
from here and may be hosted externally.

Also related: [agent-mcp](https://github.com/VanL/agent-mcp) — MCP tooling and
related agent-facing infrastructure.

## Layout

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Agent entry (permissions, conventions, read order) |
| `CLAUDE.md` | Symlink alias → `AGENTS.md` |
| `docs/program-theory.md` | This repository's program theory (replace in product repos) |
| `docs/specs/02-agent-theory-and-program-theory.md` | Definitional primer: Agent Theory + program theory (reference) |
| `docs/agent-context/` | Shared context and runbooks |
| `docs/specs/` | Process contracts and definitional reference specs |
| `docs/plans/` | Dated execution plans |
| `docs/implementation/` | Rationale and maps for this system |
| `skills/` | Task-scoped workflows |
| `bin/bootstrap-agent-theory` | Scaffold installer |
| `docs/lessons.md` | Lessons ledger |
| `docs/coalescing.md` | Coalescing state |

## Crystallizing product or module theory

```text
skills/crystallize-program-theory/SKILL.md
```

Interview the owner one decision at a time. Outcomes:

- **Product theory** — replace `docs/program-theory.md` (apex shared language).
- **Module theory** — extend the model at the module root when depth is local;
  wire entry so agents load it **on entry to that module**.

Both are the same skill and spine; the scope (product vs module) is an explicit
decision in the interview.

## Current state

This repository is the reference operating model (and its own dogfood). It does
not ship application product code. Consumer dogfood drives revisions.
