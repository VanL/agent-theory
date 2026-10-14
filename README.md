# Agent Theory

**Delegate implementation, not understanding.**

Agent Theory is a practical discipline for building software with coding
agents while keeping humans in possession of the program's theory: what the
system is, why it has its shape, what it refuses to do, and how changes are
proved.

You do not need a complete design before you write code. A program's theory
starts small and grows feature by feature through owner dialogue,
specifications, implementation, independent review, and test evidence.

This repository is the **reference operating model and starter kit** for
using Agent Theory in a codebase. In prose, the discipline is **Agent Theory**
(no hyphen); the repository and command name are `agent-theory`.

## The problem Agent Theory solves

Coding agents can write working code faster than humans can build a mental
model of how the system fits together. Left unchecked, a codebase keeps growing
after neither the human owner nor the agents understand the whole system. Each
pull request makes local sense in its own diff while quietly eroding the
product's architecture and boundaries.

Agent Theory treats human understanding as a required deliverable of every
change, not an optional side effect that might survive the next refactor. Three
ideas shape the workflow:

- **Peter Naur (*Programming as Theory Building*, 1985)** — Programming is the
  act of building a working mental model ("theory") of how the problem and the
  software fit together. Source code and documentation help transfer that
  model, but they never replace a human who holds it.
- **Donald Knuth (*Literate Programming*, 1984)** — Explanations should be
  written for human understanding and kept tied to the running code. Instead of
  putting everything in one master literate file, Agent Theory links separate
  files for theory, specs, plans, implementation notes, and code.
- **Armin Ronacher (*"The Tower Keeps Rising"*, 2026)** — Coding agents remove
  the day-to-day conversations that used to force a team to agree on shared
  concepts and boundaries. Agent Theory puts deliberate checkpoints back where
  product identity and safety are at stake.

New to the terminology? Read the short primer in
[`docs/specs/02-agent-theory-and-program-theory.md`](docs/specs/02-agent-theory-and-program-theory.md).
To see how this repository defines its own scope and non-goals, read
[`docs/program-theory.md`](docs/program-theory.md).

## How the documents divide the work

Every document type in an Agent Theory repository answers one specific
question. Keeping these roles separate prevents files from turning into
unmaintainable catch-alls:

| Document | Question it answers |
|----------|---------------------|
| **Program theory** (`docs/program-theory.md`) | What kind of system is this, who owns each concept, and what do we refuse to build? |
| **Product specs** (`docs/specs/`) | What exact behavior and invariants must hold right now? |
| **Operating-model spec** (`[DOM-*]`) | How do humans and agents classify, plan, review, verify, and maintain work? |
| **Shared agent context** (`docs/agent-context/`) | What rules and runbooks should an agent load at the start of a session? |
| **Implementation docs** (`docs/implementation/`) | Why is the current code structured this way, and where are the main edit points? |
| **Plans, reviews, and lessons** (`docs/plans/`, `docs/lessons.md`) | How are we executing an in-flight change, and what mistakes must we not repeat? |
| **Skills** (`skills/`) | How do we run recurring workflows like independent reviews, debugging, or coalescing? |
| **Bootstrap and gates** (`bin/`) | How do we install this structure into a repo and check that docs and links stay honest? |

## How a change flows from idea to commit

In day-to-day work, humans and agents follow a six-step loop that scales its
ceremony to the risk of the change:

1. **Orient on the theory (`[DOM-2]`, `[DOM-3]`).** At session start, the agent
   reads `AGENTS.md`, `docs/program-theory.md`, and the shared context in
   `docs/agent-context/`. Normative guidance is trusted from the **base
   revision**; guidance edits on a task branch are review material until
   approved. Before planning a feature, review, or audit, the agent checks
   whether the request fits the product's theory or crosses a recorded non-goal.
2. **Classify the task (`[DOM-15]`).** Every task declares a class from `0` to
   `5`. Small, reversible changes where no `[DOM-5]` non-trivial or risky
   trigger fires (Classes `1–2`) go straight to code and tests and record their
   plan in the commit message or handoff report. Work that triggers `[DOM-5]`
   non-trivial, risky, or contract rules (Classes `3–5`) starts with a dated
   plan in `docs/plans/`.
3. **Update the spec and harden the plan.** When intended behavior changes
   materially, the spec in `docs/specs/` is updated before or alongside the
   code. Risky changes (concurrency, persistence, public contracts, rollouts,
   or one-way doors) must also answer the checklist in
   `docs/agent-context/runbooks/hardening-plans.md`.
4. **Run an independent review (`[DOM-11]`).** Non-trivial plans and completed
   changes are reviewed by a different model family (for example, `codex`
   reviewing `claude` or `gemini`) using `skills/call-agent/SKILL.md`. The
   reviewer checks the plan's premises against the real code and verifies that
   the tests can actually fail.
5. **Verify with executable gates (`[DOM-10]`).** Work is not done until the
   test suite and documentation gates pass from the current working tree, and
   specs, plans, implementation notes, and code match.
6. **Report surprises and coalesce old records (`[DOM-14]`).** When code or an
   agent behaves unexpectedly, the agent surfaces the surprise to the owner and
   records a reusable rule in `docs/lessons.md`. When completed plans and dated
   lessons accumulate past the thresholds in `docs/coalescing.md`, an
   authorized coalescing sweep distills them into permanent guidance and
   retires the old plans.

For the full process rules, see
`docs/specs/01-development-documentation-operating-model.md`.

## Install into another repository

Run the bootstrap script to copy the starter files into a target repository:

```bash
./bin/bootstrap-agent-theory /path/to/target-repo
```

- **Safe by default.** The installer only creates missing files. Pass
  `--dry-run` to preview what it will write, or `--force` when you intentionally
  want to overwrite existing scaffold files.
- **No magic merges.** The installer never overwrites your existing `AGENTS.md`
  by default and never invents product architecture for you.
- **Replace the theory stub before committing product changes.** The installer
  places a short `Status: Stub` placeholder at `docs/program-theory.md` so the
  hub's own theory is never mistaken for your product's identity. You can
  explore and prototype while the file is a stub, but do not commit
  product-scope behavior or architecture treating the stub (or hub theory) as
  product authority. Use `skills/crystallize-program-theory/SKILL.md` to
  interview the owner and write your product's theory. Product-scope Class 5
  work requires at least a current `Draft` account, revised as implementation
  exposes new facts.

The installer also copies three verification scripts into `bin/`:

- `bin/check-dom15-fixtures` — verifies that the `[DOM-15]` task-classification
  table in the operating-model spec stays intact
- `bin/check-doc-paths` — verifies that backticked `docs/`, `skills/`, and
  `bin/` file paths in guidance docs actually exist
- `bin/coalesce-check` — verifies that commit SHAs and retrieval cues in
  `docs/coalescing.md` resolve in Git history

## Where humans and agents should start

| Reader | Recommended reading order |
|--------|---------------------------|
| **Humans** | This `README.md` → `docs/README.md` → `docs/specs/02-agent-theory-and-program-theory.md` → `docs/specs/01-development-documentation-operating-model.md` |
| **Agents** | `AGENTS.md` → `docs/program-theory.md` → the numbered read order in `docs/agent-context/README.md` |

Keep your product's `docs/program-theory.md` short so every session can read it
quickly. When a specific package or subsystem needs its own ownership table,
design rule, or non-goals, write a **module theory** file (`MODULE-THEORY.md`)
inside that module's directory. Agents load a module theory **on entry to that
module** (whether for design, review, audit, or implementation), not at every
session start (see [`docs/program-theory.md`](docs/program-theory.md)
`[AT-THEORY-2.1]`).

## Writing a product or module theory

Use the crystallization skill to turn tacit owner knowledge into a short,
usable theory document:

```text
skills/crystallize-program-theory/SKILL.md
```

The skill interviews the owner one question at a time, looking up repository
facts on its own and asking the human only for design decisions and refusals.
Use the same skill whether you are writing the top-level product theory
(`docs/program-theory.md`) or a local module theory (`<module>/MODULE-THEORY.md`).

## Where these practices came from

The workflow in this repository grew out of day-to-day agent-assisted
engineering on [SimpleBroker](https://github.com/VanL/simplebroker) and a
larger private codebase. We extracted the common operating model into
`agent-theory`, used it from day one to build [Taut](https://github.com/VanL/taut)
and [Backstitch](https://github.com/VanL/backstitch), and folded lessons back
between the hub, SimpleBroker, and [Weft](https://github.com/VanL/weft).

We list those repositories to show where these rules were tested in practice,
not as a controlled benchmark claim. Essays or case studies comparing Agent
Theory with other workflows belong in external writing that cites this
repository.

Related tooling: [agent-mcp](https://github.com/VanL/agent-mcp) provides MCP
servers and agent-facing infrastructure used alongside these repositories.

## Repository layout

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Primary agent entry point (permissions, read order, conventions) |
| `CLAUDE.md` | Symlink alias to `AGENTS.md` |
| `docs/program-theory.md` | Program theory for this hub repository (replaced in product repos) |
| `docs/specs/02-agent-theory-and-program-theory.md` | Definitional primer explaining Agent Theory and program theory |
| `docs/agent-context/` | Shared context, principles, and operational runbooks |
| `docs/specs/` | Process contracts (`[DOM-*]`) and reference definitions |
| `docs/plans/` | Dated execution plans and status index |
| `docs/implementation/` | Design rationale, repository map, and agent inventory |
| `skills/` | Reusable step-by-step workflows |
| `bin/bootstrap-agent-theory` | Installer that copies the starter scaffold into another repo |
| `docs/lessons.md` | Golden rules and dated lessons learned |
| `docs/coalescing.md` | Watermarks, thresholds, and run log for coalescing sweeps |

## Current state

This repository maintains the reference operating model and tests its own gates
and coalescing rules on itself. It does not ship application code; lessons from
the product repositories above drive revisions here.
