# Agent Context Hub

This folder is the canonical shared context for coding agents, automation
agents, and human contributors working in this repository.

## Goals

- Keep one repo-owned source of truth for durable execution standards.
- Reduce drift across agent-specific root files.
- Make planning, testing, and documentation maintenance explicit.
- Make review loops, agent bootstrap, and skill maintenance explicit.
- Keep spec, plan, implementation, and code traceability bidirectional.

## Read Order

For **this hub repository**, start with the conceptual account, then process.
This list omits this file (you are reading it); root `AGENTS.md` names the
same sequence with this file as its own step, so its numbering runs one
ahead from step 2 onward. The two lists are the same order, not two orders.

1. `../program-theory.md` — what agent-theory is (Naur / Knuth / Ronacher
   lineage; **module theory as the concrete extension of product theory**;
   consumer replacement rule)
2. `decision-hierarchy.md`
3. `principles.md`
4. `engineering-principles.md`
5. Relevant runbook(s) in `runbooks/`
6. `lessons.md`
7. `../lessons.md` — required startup reading is the **Golden Rules section
   plus dated entries after the lessons watermark** (see `../coalescing.md`).
   Older entries are searchable reference material, not startup context.

Machine-readable order: `context.index.yaml` `read_order`.

## Runbooks

- `writing-plans.md`: how to write executable implementation plans (including
  spec baseline, proposed spec delta, promotion slices, and status
  mechanisms)
- `hardening-plans.md`: required companion for risky or boundary-crossing plans
  that must survive review
- `review-loops-and-agent-bootstrap.md`: how to bootstrap available agents and
  run independent plan/work reviews
- `writing-specs.md`: how to define intended behavior with stable references
- `writing-implementation-docs.md`: how to capture rationale and boundaries
- `testing-patterns.md`: how to choose the right proof and avoid weak tests
- `adversarial-acceptance-probes.md`: the black-box probe kit any
  implementation must pass before integration, independent of spec version
- `maintaining-traceability.md`: how to keep docs synchronized during delivery
- `skills-lifecycle.md`: how to add, update, and retire reusable skills
- `designing-agent-facing-interfaces.md`: principles for designing APIs,
  CLIs, and docs that agents consume
- `external-skill-suites.md`: precedence and crosswalk for external skill
  suites (superpowers, gstack, Every's compound engineering)

## What Belongs Here

- durable decision policies
- reusable engineering workflow guidance
- short pointers into the canonical lessons ledger

## What Does Not Belong Here

- product or architecture specs that define the system itself
- one-off execution notes for a single task
- agent-vendor-specific syntax that is not reusable across tools

## Maintenance Rules

- Keep files short, operational, and repository-owned.
- Prefer checklists and direct rules over long prose.
- When a repeated mistake shows up, add a lesson in `../lessons.md` and
  strengthen a runbook if the fix should become reusable guidance.
- When plans keep failing at boundaries, strengthen `writing-plans.md` or
  `runbooks/hardening-plans.md` instead of leaving the correction trapped in a
  single plan.
- When a repeated workflow becomes stable and reusable, promote it into a skill
  under `../skills/`.
- When `docs/coalescing.md` shows a tripped threshold, report it and
  respond per [DOM-14]: a checked-deferred line with derived counts, or a
  full sweep (its own unit of work) on user request, at twice the
  threshold, or at a completion boundary. The session-start check itself is
  read-only.
