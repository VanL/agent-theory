# Specs Index Renumbering

Status: Completed 2026-04-07

## Goal

Make the specs directory follow the same numbering pattern as the
implementation docs: `00` should be the numbered entry index, and the current
operating-model spec should move to `01`.

## Source Documents

Source spec:

- `docs/specs/01-development-documentation-operating-model.md` [DOM-2],
  [DOM-3], [DOM-4], [DOM-8]

Read first:

- `AGENTS.md`
- `README.md`
- `docs/specs/00-specs-index.md`
- `docs/implementation/00-implementation-index.md`
- `docs/plans/2026-04-07-bootstrap-scaffold-plan.md`

## Context and Key Files

Files to modify:

- `AGENTS.md`
- `README.md`
- `docs/README.md`
- `docs/specs/README.md`
- `docs/implementation/01-documentation-system.md`
- `docs/implementation/02-repository-map.md`
- `docs/implementation/03-agent-inventory.md`
- `docs/agent-context/principles.md`
- `docs/plans/2026-04-07-development-documentation-foundation-plan.md`
- `docs/plans/2026-04-07-review-skills-bootstrap-plan.md`
- `docs/plans/2026-04-07-plan-hardening-guidance-plan.md`
- `docs/plans/2026-04-07-bootstrap-scaffold-plan.md`
- `bin/bootstrap-agent-theory`

Files to add:

- `docs/specs/00-specs-index.md`

Files to rename:

- `docs/specs/00-development-documentation-operating-model.md`
  -> `docs/specs/01-development-documentation-operating-model.md`

Shared boundaries:

- keep `README.md` in `docs/specs/` as a thin pointer to the numbered index
- repair path references everywhere instead of leaving stale historical links
- keep the DOM reference codes unchanged

## Invariants and Constraints

- This is a documentation-structure change only; do not change the substance
  of the operating-model requirements.
- `00` in `docs/specs/` should become the canonical index, not a competing
  second overview.
- Historical plans should retain working links even after the rename.
- The bootstrap scaffold must install the same numbering pattern into target
  repositories.

## Tasks

1. Add the numbered specs index and shift the operating-model spec to `01`.
   - Files to touch:
     - `docs/specs/README.md`
     - `docs/specs/00-specs-index.md`
     - `docs/specs/01-development-documentation-operating-model.md`
   - Outcome:
     - specs now have the same numbered-entry pattern as implementation docs
   - Tests:
     - confirm `README.md` points to the numbered index
     - confirm the operating-model spec lives at `01-...`

2. Repair all repository references to the renamed spec path and the new spec
   index.
   - Files to touch:
     - root docs and implementation docs
     - affected dated plans
   - Outcome:
     - no stale `00-development-documentation-operating-model.md` references
       remain
   - Tests:
     - grep for old and new spec paths

3. Update the bootstrap scaffold to install the new specs layout.
   - Files to touch:
     - `bin/bootstrap-agent-theory`
     - `docs/plans/2026-04-07-bootstrap-scaffold-plan.md`
   - Outcome:
     - fresh installs get `docs/specs/00-specs-index.md` and
       `docs/specs/01-development-documentation-operating-model.md`
   - Tests:
     - scaffold into a throwaway target and inspect the resulting `docs/specs/`
       tree

4. Run review and record the result.
   - Files in scope:
     - all touched files above
   - Outcome:
     - the renumbering is reviewed before closeout
   - Tests:
     - record accepted and rejected findings in this plan

## Testing Plan

Use grep-based checks plus a real scaffold smoke test.

Checks:

- no references to the old `00-development-documentation-operating-model.md`
  path remain
- the new `00-specs-index.md` is referenced from root entry points and the
  scaffold
- the scaffold creates the new spec numbering in a throwaway target

## Verification and Gates

Run:

```bash
rg -n "00-development-documentation-operating-model" AGENTS.md README.md docs/specs docs/implementation bin
rg -n "00-specs-index|01-development-documentation-operating-model" AGENTS.md README.md docs/specs docs/implementation bin
rm -rf /tmp/agent-theory-specs-smoke
./bin/bootstrap-agent-theory /tmp/agent-theory-specs-smoke
find /tmp/agent-theory-specs-smoke/docs/specs -maxdepth 1 -type f | sort
```

Success looks like:

- the first `rg` command prints no matches; `docs/plans/` is intentionally
  excluded because this plan records the historical rename
- the second `rg` command prints matches in the expected entry points, spec
  files, implementation docs, and scaffold script
- the scaffolded target gets the renamed spec files

## Independent Review Loop

Use an independent reviewer after the renumbering and scaffold changes form one
coherent slice.

Review prompt:

> Read the plan at [path]. Carefully examine the plan and the associated code.
> Look for errors, bad ideas, and latent ambiguities. Don't do any
> implementation, but answer carefully: Could you implement this confidently and
> correctly if asked?

Review result:

- 2026-04-07 Claude review found one substantive issue: the plan read like
  future work even though the rename and reference updates were already done in
  the working tree. Accepted and fixed by marking this plan completed and
  making the verification expectations explicit.
- The same review also suggested clarifying that the old-path grep is scoped to
  exclude `docs/plans/` so the plan's own historical rename record does not
  create a false positive. Accepted and fixed.
- The reviewer confirmed the core behavior: `00` is clearly the canonical
  specs index, `docs/specs/README.md` is only a pointer, and the scaffold
  installs the new spec layout correctly.
- A follow-up Claude review on the revised slice reported no blocker or
  medium-severity issues and confirmed the slice is coherent and implementable.
- No blocker findings remain.

## Out of Scope

- changing DOM reference codes
- changing the operating-model content beyond path and index references
- adding more specs beyond the new index file
