# Plan Hardening Guidance Plan

Status: Completed 2026-04-07

## Goal

Strengthen the repository's planning guidance so implementation plans are not
just structurally complete, but explicitly hardened against the failure modes
that cause review churn and implementation drift: missing invariants, hidden
couplings, weak testing guidance, vague rollout/rollback, and under-specified
boundaries.

## Source Documents

Source specs:

- `docs/specs/00-development-documentation-operating-model.md` [DOM-5],
  [DOM-8], [DOM-10], [DOM-11]

External input:

- `/Users/van/Downloads/planning-guidance.md`

Extracted themes from the external input:

- state invariants before tasks
- identify hidden couplings before decomposition
- separate wrapper logic from core work
- add stop-and-re-evaluate gates
- state out-of-scope explicitly
- specify what must not be mocked
- test contracts and durable behavior, not only internals
- make fatal versus best-effort error priorities explicit
- define observable success after deploy
- describe the current file or contract, not only the file path
- think through rollout sequencing, one-way doors, and deferred-input lifecycle
- write rollback early enough to shape the plan
- require reading with comprehension checks on risky work

Read first:

- `AGENTS.md`
- `README.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/hardening-plans.md`
- `docs/agent-context/runbooks/maintaining-traceability.md`
- `docs/agent-context/README.md`
- `docs/README.md`

## Context and Key Files

Files to modify:

- `AGENTS.md`
- `README.md`
- `docs/agent-context/README.md`
- `docs/agent-context/principles.md`
- `docs/agent-context/engineering-principles.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/hardening-plans.md`
- `docs/specs/00-development-documentation-operating-model.md`
- `docs/README.md`
- `docs/plans/README.md`
- `docs/implementation/00-documentation-system.md`
- `docs/implementation/01-repository-map.md`
- `docs/lessons.md`

Style and guidance:

- `docs/agent-context/principles.md`
- `docs/agent-context/engineering-principles.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/hardening-plans.md`

Reuse:

- keep `writing-plans.md` as the primary operational entry point
- keep deeper rationale in a dedicated companion runbook rather than bloating
  every other doc

Current roles:

- `AGENTS.md` and `README.md` are session-start and repository-entry surfaces
- `docs/agent-context/README.md`, `principles.md`, and
  `engineering-principles.md` are shared startup policy docs
- `docs/agent-context/runbooks/writing-plans.md` is the main operational
  planning runbook
- `docs/agent-context/runbooks/hardening-plans.md` is the companion runbook
  for risky-work rewrite criteria and examples
- `docs/specs/00-development-documentation-operating-model.md` is the governing
  documentation contract
- `docs/README.md`, `docs/plans/README.md`, and the implementation notes are
  navigational and explanatory surfaces
- `docs/lessons.md` is the durable rule ledger

## Invariants and Constraints

- This is a docs/process change only; do not add product-specific planning
  content.
- The guidance should stay project-neutral and usable outside the source
  codebase that inspired it.
- The result should be more prescriptive, not more verbose for its own sake.
- The main runbook should stay directly operational; deeper rationale can live
  in a companion runbook.
- The setup should still clearly prefer runbooks over skills for repo-wide
  planning process.
- The session-start agent context should surface the stronger planning rules,
  not hide them only in deep docs.

## Tasks

1. Update the governing planning requirements in the spec.
   - Outcome: the spec names the plan-hardening expectations explicitly.
   - Files to touch:
     - `docs/specs/00-development-documentation-operating-model.md`
   - Read first:
     - current [DOM-5] and [DOM-10]
   - Update:
      - add hardening expectations such as invariants-before-tasks,
       hidden-coupling visibility, anti-mocking guidance, rollback/rollout, and
       observable success criteria when relevant
   - Tests:
     - inspect the spec for exact, reusable wording rather than essay prose
   - Done when:
     - the spec names the planning contract briefly and points to the planning
       runbooks for operational detail instead of duplicating them

2. Surface the stronger planning rules from the session-start docs.
   - Outcome: agents encounter the planning bar before they start freeforming.
   - Files to touch:
     - `AGENTS.md`
     - `README.md`
     - `docs/agent-context/README.md`
     - `docs/agent-context/principles.md`
     - `docs/agent-context/engineering-principles.md`
   - Update:
     - `AGENTS.md`: add the risky-work trigger and definition-of-done reminder
     - `README.md`: add the top-level expectation that risky plans are hardened
       before implementation
     - `docs/agent-context/README.md`: mark the hardening runbook as required
       on risky work
     - `docs/agent-context/principles.md`: add the over-prescriptive planning
       rule and proof expectations
     - `docs/agent-context/engineering-principles.md`: add a boundary-first
       planning principle and warning signs
   - Tests:
     - inspect the entry-point docs for short, durable language that points to
       the deeper runbooks
   - Done when:
     - a new agent sees the stronger planning standard from the normal read
       order

3. Make the primary planning runbook define the required plan shape for risky
   work.
   - Outcome: `writing-plans.md` tells the implementer exactly what the plan
     must contain before coding starts.
   - Files to touch:
     - `docs/agent-context/runbooks/writing-plans.md`
   - Read first:
     - `/Users/van/Downloads/planning-guidance.md`
   - Update:
     - define when hardening is mandatory
     - tighten the required sections for current-structure context, invariants,
       anti-mocking posture, rollback/rollout, and post-deploy signals
     - add explicit blockers before implementation for risky work
     - state the role split between this runbook and `hardening-plans.md`
   - Tests:
     - inspect the runbook for operational checklist items rather than generic
       planning advice
   - Done when:
     - a zero-context engineer would know what a structurally strong plan still
       needs before it is review-ready

4. Make the companion plan-hardening runbook carry the rewrite criteria and
   examples for risky work.
   - Outcome: the deeper reasoning and checklist live in one reusable place and
     act as a hard gate for risky work without replacing `writing-plans.md`.
   - Files to touch:
     - `docs/agent-context/runbooks/hardening-plans.md`
   - Read first:
     - `/Users/van/Downloads/planning-guidance.md`
   - Constraints:
     - keep it operational
      - avoid source-codebase-specific jargon
   - Tests:
     - inspect for concise sections and reusable examples
   - Done when:
     - the repo has a dedicated reference for turning first-draft plans into
       review-surviving plans and blocking under-specified risky work

5. Wire the stronger planning guidance into the repo indexes, implementation
   notes, and lessons.
   - Outcome: the new guidance is discoverable and documented as a durable
     standard.
   - Files to touch:
     - `docs/README.md`
     - `docs/plans/README.md`
     - `docs/implementation/00-documentation-system.md`
     - `docs/implementation/01-repository-map.md`
     - `docs/lessons.md`
   - Tests:
     - inspect that planning entry points now mention the hardening material
   - Done when:
     - another engineer can discover the new guidance without knowing it exists

6. Run an independent review and answer the findings.
   - Outcome: the new guidance itself survives an external review pass.
   - Files in scope:
     - all changed planning-guidance files
   - Review timing:
     - run the review after the spec, session-start docs, and both planning
       runbooks form one coherent slice
     - if that review forces structural change, run one follow-up review on the
       revised slice before calling the work complete
   - Tests:
     - collect findings and update docs or explain no-change decisions
   - Done when:
     - the review feedback loop is reflected in the final docs or in this plan

## Testing Plan

This is a docs-only change. Verification is by inspection and targeted
grep-based checks.

Checks:

- the spec names the stronger planning requirements
- the planning runbook contains explicit hardening guidance
- the companion runbook is treated as required for risky work
- session-start docs surface the stronger planning rules
- the language stays project-neutral and operational

## Verification and Gates

Run:

```bash
find docs/agent-context/runbooks docs/plans docs/specs docs/implementation -type f | sort
rg -n "hardening-plans" AGENTS.md README.md docs
rg -n "hidden couplings?|what must not change|one-way doors?|rollback|rollout|observable success|comprehension questions?" docs
rg -n "stop-and-re-evaluate|what should not be mocked|post-deploy" docs/agent-context/runbooks/writing-plans.md docs/specs/00-development-documentation-operating-model.md docs/agent-context/runbooks/hardening-plans.md
rg -n " +$|\t+$|^<<<<<<<|^=======|^>>>>>>>" docs README.md AGENTS.md CLAUDE.md || true
```

Success looks like:

- the new hardening guidance appears in the intended docs
- the required-entry docs point to the stronger planning standard
- the whitespace and merge-marker check prints no matches

## Independent Review Loop

Reviewer preference:

1. a different agent family than Codex
2. if not available, another available reviewer path with explicit limitation

Reviewer inputs:

- this plan
- `/Users/van/Downloads/planning-guidance.md`
- `AGENTS.md`
- `README.md`
- `docs/README.md`
- `docs/agent-context/README.md`
- `docs/agent-context/principles.md`
- `docs/agent-context/engineering-principles.md`
- `docs/agent-context/runbooks/writing-plans.md`
- `docs/agent-context/runbooks/hardening-plans.md`
- `docs/specs/00-development-documentation-operating-model.md`
- `docs/plans/README.md`
- `docs/implementation/00-documentation-system.md`
- `docs/implementation/01-repository-map.md`
- `docs/lessons.md`

Review prompt:

> Read the plan at [path]. Carefully examine the plan and the associated code.
> Look for errors, bad ideas, and latent ambiguities. Don't do any
> implementation, but answer carefully: Could you implement this confidently and
> correctly if asked?

Feedback handling:

- update the docs for accepted findings
- record no-change decisions for rejected findings
- treat a reviewer confidence failure as a blocker

Review result:

- Claude review findings accepted:
  - specify the prose transformation more concretely because docs are the
    deliverable
  - make the task split across session-start docs explicit file by file
  - avoid depending on the external note as an opaque absolute-path input by
    summarizing the extracted themes in this plan
  - clarify the role split between the governing spec, `writing-plans.md`, and
    `hardening-plans.md`
  - improve verification greps and review timing language
- Claude review findings accepted with limited change:
  - add current-role summaries for touched files in this plan rather than
    bloating every task with repeated file descriptions
- Claude review findings not adopted fully:
  - the external note remains listed as source material because it was the
    actual input, but the plan now also summarizes the extracted rules so the
    work is not blocked on that path alone
- Claude follow-up review finding accepted:
  - add the missing backlink from
    `docs/specs/00-development-documentation-operating-model.md` to this plan
  - align the risky-change wording in the spec more closely with the runbooks
- Final confidence:
  - after the revisions above, the review concerns are addressed and the plan
    now constrains the docs-as-deliverable work tightly enough for confident
    implementation

## Out of Scope

- adding a planning skill
- introducing product-specific planning templates
- building plan-evaluation automation or CI enforcement

## Fresh-Eyes Review

Re-read the updated planning docs as a zero-context engineer and ask:

- is the split between governing spec, main planning runbook, and hardening
  runbook clear enough that I would not duplicate content by accident?
- do the session-start docs tell me when hardening is mandatory, or would I
  still have to discover that later?
- do the plan tasks constrain prose edits file by file, or am I still making
  editorial guesses?
- could I follow the verification and review loop without inventing missing
  steps?

The final version should feel stricter, more review-proof, and more usable by
an agent than the pre-change version.
