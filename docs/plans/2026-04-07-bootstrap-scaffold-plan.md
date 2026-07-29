# Agent Guidance Bootstrap Scaffold

## Goal

Add a small, explicit bootstrap command that can scaffold this repository's
project-neutral agent-theory starter set into another repository without
trying to infer repo-specific engineering rules or merge with existing custom
docs.

## Source Documents

Source spec:

- `docs/specs/01-development-documentation-operating-model.md` [DOM-2],
  [DOM-3], [DOM-4], [DOM-7], [DOM-8]
- plus repository tooling change for distributing the guidance scaffold

Read first:

- `AGENTS.md`
- `README.md`
- `docs/implementation/00-implementation-index.md`
- `docs/implementation/01-documentation-system.md`
- `docs/implementation/02-repository-map.md`
- `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md`

## Context and Key Files

Files to modify:

- `README.md`
- `docs/implementation/README.md`
- `docs/implementation/01-documentation-system.md`
- `docs/implementation/02-repository-map.md`

Files to add:

- `bin/bootstrap-agent-theory`
- `docs/implementation/00-implementation-index.md`
- `docs/plans/2026-04-07-bootstrap-scaffold-plan.md`

Shared paths and boundaries:

- the scaffold should copy only the reusable starter corpus, not this repo's
  historical dated plans
- root alias behavior should match the existing `CLAUDE.md -> AGENTS.md`
  symlink rule
- the script should stay create-only by default and require an explicit flag
  to overwrite existing files

## Invariants and Constraints

- Keep the script intentionally non-magical.
- Do not infer repo-specific engineering principles, test commands, or product
  architecture from the target repo.
- Do not try to merge into an existing `AGENTS.md`.
- Default behavior should be safe in a dirty or already-customized target repo.
- The script should support dry-run mode and print a manual follow-up checklist.
- The script should refuse to target the source repository itself.
- The script should fail fast if the source scaffold corpus is incomplete.

## Tasks

1. Add the bootstrap command.
   - Files to touch:
     - `bin/bootstrap-agent-theory`
   - Outcome:
     - a target repo can receive the reusable scaffold with one command
   - Required behavior:
     - accept a target directory argument
     - support `--dry-run`
     - support an explicit overwrite flag
     - copy only the curated starter files
     - create `CLAUDE.md` as a symlink to `AGENTS.md` when possible, with a
       thin pointer-file fallback if symlinks are unavailable
     - refuse to scaffold into the source repository itself
     - validate that the required source files exist before copying anything
     - print which files were created, skipped, or overwritten
     - print manual follow-up steps for repo-specific adaptation, including
       `AGENTS.md`, `docs/README.md`, overwrite risk, and non-transactional
       behavior
   - Stop and re-evaluate if:
     - the implementation starts trying to parse or rewrite existing target
       docs beyond create-or-overwrite behavior

2. Document the bootstrap flow.
   - Files to touch:
     - `README.md`
     - `docs/implementation/README.md`
     - `docs/implementation/00-implementation-index.md`
     - `docs/implementation/01-documentation-system.md`
     - `docs/implementation/02-repository-map.md`
   - Outcome:
     - the repo clearly explains that it now includes a scaffold command and
       what it does not attempt to automate
   - Tests:
     - document the command line, the create-only default, and the manual
       adaptation expectations

3. Verify and review the change.
   - Files in scope:
     - all touched files above
   - Outcome:
     - the script works on a throwaway target and the docs match its actual
       behavior
   - Tests:
     - run the script against a temporary directory
     - run it again without `--force` to prove skip behavior
     - run it with `--dry-run`
     - inspect the scaffolded tree and the `CLAUDE.md` alias behavior
     - run an independent review on the touched slice and answer the findings

## Testing Plan

Use a real temporary target directory rather than mocks.

Checks:

- `bin/bootstrap-agent-theory --dry-run <tmpdir>` shows the planned actions
- `bin/bootstrap-agent-theory <tmpdir>` creates the expected scaffold
- a second run without overwrite skips existing files cleanly
- `CLAUDE.md` is a symlink to `AGENTS.md` or a clear pointer fallback if
  symlinks fail
- the script rejects the source repo as a target
- README and implementation docs describe the actual command and scope limits

## Verification and Gates

Run:

```bash
./bin/bootstrap-agent-theory --dry-run /tmp/agent-theory-smoke
rm -rf /tmp/agent-theory-smoke
./bin/bootstrap-agent-theory /tmp/agent-theory-smoke
./bin/bootstrap-agent-theory /tmp/agent-theory-smoke
find /tmp/agent-theory-smoke -maxdepth 3 -type f -o -type l | sort
ls -l /tmp/agent-theory-smoke/CLAUDE.md
! ./bin/bootstrap-agent-theory .
python3 -m py_compile bin/bootstrap-agent-theory
```

Success looks like:

- the dry run reports planned creates without writing files
- the real run creates the scaffolded files and alias
- the second real run reports skips rather than overwriting
- self-targeting is rejected explicitly
- the script is syntactically valid
- the docs reference the command accurately

## Independent Review Loop

Use an independent reviewer after the script and docs form one coherent slice.

Review prompt:

> Read the plan at [path]. Carefully examine the plan and the associated code.
> Look for errors, bad ideas, and latent ambiguities. Don't do any
> implementation, but answer carefully: Could you implement this confidently and
> correctly if asked?

Review result:

- 2026-04-07 Claude review found useful gaps: no self-target guard, no
  scaffold-source validation, follow-up guidance that missed `AGENTS.md` and
  `docs/README.md`, weak overwrite/update warnings, and an overly indirect
  source-spec statement in this plan. Accepted and fixed.
- 2026-04-07 follow-up Claude review said the scaffold could be implemented
  confidently and correctly. Remaining notes were low-risk: safer `--force`
  behavior around directories, clearer rerun guidance for partial failures, a
  less fragile self-target verification command, and a note that extra
  tool-specific aliases remain manual. Accepted and fixed.
- No blocker findings remain after the review-driven edits.

## Out of Scope

- automatic merging into customized target repos
- detecting or rewriting repo-specific test commands
- synchronizing updates into already-installed repos
- packaging this as a pip/npm installer
