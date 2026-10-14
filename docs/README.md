# Documentation Guide

This repository uses a docs-first workflow so humans and coding agents share one
source of truth for system identity, intended behavior, in-flight plans, and
lessons learned.

## Directory Structure

Each directory or top-level file answers one specific question:

- `program-theory.md`: what kind of system **this repository** is, who owns its
  core concepts, what it refuses to build, and what evidence would show that
  model is wrong
- `agent-context/`: shared rules, principles, and runbooks loaded by agents at
  session start
- `specs/`: behavioral contracts (intended behavior, invariants, and
  verification) plus reference definitions such as
  `specs/02-agent-theory-and-program-theory.md`
- `plans/`: dated execution plans for non-trivial changes, tracked in
  `plans/README.md`
- `implementation/`: design rationale, ownership boundaries, repository maps,
  and agent availability
- `../skills/`: step-by-step instructions for recurring workflows
- `lessons.md`: golden rules and dated corrections from past mistakes
- `coalescing.md`: thresholds, watermarks, and run log for periodic
  distillation of completed plans and lessons
- `lore/`: dated primary-source records (external-session transcripts,
  prediction/confirmation notes) kept for origin context; historical, never
  normative — promoted conclusions live in theory, specs, or lessons

## What to Read by Task

### Understanding Agent Theory and Program Theory

Read these on demand when onboarding or before drafting a theory file (not at
every session start):

- `specs/02-agent-theory-and-program-theory.md` — short primer defining the
  terms and how the documents fit together
- `program-theory.md` — the working theory of **this repository** (describes the
  product in a product repository, or the guidance system in the Agent Theory
  hub)
- `../skills/crystallize-program-theory/SKILL.md` — one-question-at-a-time
  interview for writing a product or module theory

### Starting a Session

Read in this order:

1. `../AGENTS.md`
2. `program-theory.md` — the conceptual identity of **this repository**. If its
   status is `Stub`, replace it before committing product-scope behavior or
   architecture (use `../skills/crystallize-program-theory/SKILL.md`). Humans
   may skim `../README.md` first.
3. `agent-context/README.md` and the shared context files it lists
4. `implementation/03-agent-inventory.md`, if present
5. The governing spec in `specs/`
6. The active plan in `plans/`, if one exists
7. The relevant rationale note in `implementation/`
8. The relevant workflow in `../skills/`, if one exists

### Planning a Non-Trivial Change (Classes 3–5)

Read:

- `agent-context/runbooks/writing-plans.md`
- `agent-context/runbooks/hardening-plans.md` (required for risky or
  boundary-crossing changes)
- `agent-context/runbooks/review-loops-and-agent-bootstrap.md`
- `agent-context/runbooks/maintaining-traceability.md`

Write a dated plan in `plans/YYYY-MM-DD-<slug>.md` and add a row to the status
index in `plans/README.md`.

### Writing or Updating a Spec

Read `agent-context/runbooks/writing-specs.md`. Put intended behavior,
invariants, and stable reference codes in `specs/`, and link the related plans
at the bottom of the spec.

### Explaining Why the Code Is Shaped This Way

Read `agent-context/runbooks/writing-implementation-docs.md`. Use
`implementation/` to explain design tradeoffs, ownership boundaries, and key
edit points rather than narrating the code line by line.

### Creating or Updating a Skill

Read `agent-context/runbooks/skills-lifecycle.md`. Promote a workflow into
`../skills/` once it has recurred across multiple tasks and needs a repeatable
checklist.

### Testing or Debugging

Read `agent-context/runbooks/testing-patterns.md` (and `../skills/debugging/SKILL.md`
when diagnosing a bug). Prefer tests that exercise real code paths over heavy
mocking.

## Core Documentation Standards

- **Specs own intended behavior.** Update the spec before or alongside any
  material behavior change.
- **Plans are written for zero-context engineers.** State what must *not*
  change, not only what to add.
- **Risky plans require explicit hardening.** Name hidden couplings, what must
  not be mocked, rollback or rollout order, one-way doors, and post-deploy
  checks before implementation starts.
- **Non-trivial plans and completed changes get an independent review** from a
  different model family when available.
- **Implementation docs explain *why*, not just *how*.**
- **Documentation updates are part of the completion gate**, never optional
  follow-up cleanup.
