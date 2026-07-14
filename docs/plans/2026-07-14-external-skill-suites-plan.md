# External Skill Suites Compatibility Plan

Status: Active — additive guidance; no spec delta required
Plan type: guidance addition (crosswalk runbook + two gap skills)
Risk level: low — additive files plus scaffold integration; no existing
guidance changes meaning

## 1. Goal

Make the repo's operating model explicitly compatible with the external
skill suites agents pick up naturally (superpowers, gstack, Every's
compound-engineering plugin): declare precedence, map each commonly
auto-fired skill to its governing repo doc, name the known conflicts, and
harvest the two genuine gaps (debugging discipline, brainstorm-to-plan
bridge) as repo-owned skills rather than vendored copies.

## 2. Source Documents

- `docs/specs/01-development-documentation-operating-model.md`
  [DOM-5], [DOM-10], [DOM-11], [DOM-12], [DOM-14]
- `docs/agent-context/runbooks/skills-lifecycle.md` (promotion rule)
- Survey evidence (this session): superpowers 6.0.2 skill texts
  (writing-plans, verification-before-completion, systematic-debugging,
  receiving-code-review), gstack skill set (plan-eng-review and peers),
  Every compound-engineering guide.

## 2a. Context and Key Files

- Files created: the three deliverables named in §5 tasks 1–3.
- Files edited: `bin/bootstrap-agent-guidance` (COPIED_FILES + two
  renderers), `docs/agent-context/README.md` (runbook list),
  `docs/agent-context/context.index.yaml`, `docs/plans/README.md` (status
  index), `docs/implementation/02-repository-map.md` (this repo's own
  checked-in map — distinct from the scaffold renderer).
- Read first: `decision-hierarchy.md` (precedence tiers),
  `testing-patterns.md` Rule 5 (the substitute-proof owner),
  `skills-lifecycle.md` (skills vs runbooks boundary).

## 2b. Spec Classification

No `## Proposed Spec Delta`: this plan adds operational runbook/skill
guidance under existing [DOM-11]/[DOM-12] authority and operationalizes
the existing decision-hierarchy tier ordering; it does not change intended
behavior in the spec tree. Reviewer pushback on this classification
(codex finding 8) is dispositioned in §7a; the residual disagreement —
whether process-operationalizing runbooks are [DOM-6]-material — is
escalated to the task-class-matrix follow-up rather than resolved here.

## 3. Invariants and Constraints

- **No vendored copies.** External skills are pointed to, never forked
  into `skills/` — point-in-time copies drift (the ecosystem's documented
  disease). Gap harvests are repo-owned distillations that cite their
  inspiration.
- **One canonical owner per rule.** The crosswalk assigns each overlapping
  rule to its repo home; it never restates the rule's content.
- **Precedence is declared, not assumed:** repo guidance governs when an
  external skill and a repo doc conflict. This matches superpowers' own
  priority rules (user/repo instructions above skills).
- **Known conflicts are named explicitly** (file-size guidance vs
  engineering-principles §14; plan location; TDD absolutism vs §10's
  escape hatch). A crosswalk that hides conflicts trains agents to ignore
  it.
- New skills follow the `skills/_template/SKILL.md` section order and the
  four-part owner/boundary/verification/required-action pattern.

## 4. Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## 5. Tasks

1. `docs/agent-context/runbooks/external-skill-suites.md` — the crosswalk.
2. `skills/debugging/SKILL.md` — root-cause-first debugging, distilled
   from superpowers:systematic-debugging into repo shape, tied to
   engineering-principles §10 and Golden Rule 11.
3. `skills/brainstorming-to-plan/SKILL.md` — the bridge from exploration
   to a [DOM-5] plan, including when a spec must land first.
4. Scaffold integration: all three files into COPIED_FILES; repo-map and
   documentation-system renderers updated; agent-context README runbook
   list and context.index.yaml updated; plans README status index row.
5. Verification: scaffold dry-run into scratch, backstitch self-corpus
   check, grep gates for each new file reference.

## 6. Verification and Gates

- backstitch: 0 errors, 0 warnings after all edits
- scaffold run creates the three files in a scratch target
- every path named in the new files resolves
- crosswalk table covers every superpowers skill that auto-fires on
  planning/review/verification work, and names all three known conflicts

## 7. Independent Review Loop

Executed 2026-07-14: Codex (different agent family), consult mode,
read-only against the landed files, with the three review questions from
the original stance. Codex answered no to all three; findings and
dispositions in §7a. Sequencing lesson accepted: this review should have
preceded landing for process-changing guidance (finding 9) — recorded in
`docs/lessons.md`; the mitigation is that review completed before any
propagation.

## 7a. Review Findings and Dispositions (Codex, 2026-07-14)

| # | Finding (abbrev.) | Disposition |
|---|---|---|
| 1 | No external-to-external tie-break | **Accepted.** Three-case precedence with explicit tie-break added to the runbook |
| 2 | User-invoked skill is tier-1, not inference | **Accepted.** Precedence rewritten to split user-invoked vs auto-fired |
| 3 | §10 escape hatch misattributed | **Accepted — real defect.** Substitute proof correctly attributed to testing-patterns Rule 5 in the crosswalk, known-conflicts, and debugging skill |
| 4 | Debugging skill inconsistent about proof | **Accepted.** Reproduction exception (step 1) and regression-proof substitution (Rule 5) now explicitly separate decisions |
| 5 | "Unspecified = not a bug" false | **Accepted.** Reworded: diagnose first; spec-gap classification comes after root cause |
| 6 | "No spec impact → Source spec: None" destroys traceability | **Accepted.** Classification split: unchanged-governing-spec (cite + baseline) vs no-spec-exists |
| 7 | File count is not the triviality test | **Accepted.** Triviality judged by [DOM-5] criteria, stated in the skill |
| 8 | "No spec delta" classification unsupported | **Rejected with reasoning** (§2b): operationalizes existing decision-hierarchy/[DOM-11]/[DOM-12] authority; residual disagreement escalated to task-class matrix |
| 9 | Review-after-landing sequence backward | **Accepted as lesson.** Process-changing guidance gets pre-landing review; recorded in lessons; review completed pre-propagation |
| 10 | Plan not DOM-5 compliant | **Partially accepted.** §2a/§2b added; testing plan is §6 (docs-only, inspection + named commands); the lean-vs-full tension escalated to task-class matrix — all three reviewers now demand it from opposite directions |
| 11 | Persona ≠ independent review | **Accepted.** Separate-execution requirement added to gstack row |
| 12 | Compound mapping overclaims authority | **Accepted.** Candidates-not-authorization caveats added |
| 13 | Firings as promotion evidence contradicts §15 | **Accepted.** Firings are a hint to check; citations remain the evidence |
| 14 | Harvested skills lack promotion evidence | **Rejected with reasoning.** Skill creation was an explicit tier-1 user instruction, which outranks the promotion heuristic; noted here as the authorization record |
| 15 | Coverage claim unverifiable | **Accepted.** Superpowers 6.0.2 inventory enumerated in the runbook; gstack/Every rows declared representative |
| 16 | Ambiguous refs; "§8" misattributed | **Accepted.** Path-semantics declaration added; §8 now cited as engineering-principles §8 |
| P2-1 | Debugging lacks diagnosis method | **Accepted.** Backward trace, good-vs-bad diff, one-variable falsifiable hypotheses added to step 3 |
| P2-2 | Brainstorm bridge omits spec-changing sequence | **Accepted.** Review → promote → baseline → implement spelled out |
| P2-3 | Open questions routed incorrectly | **Accepted.** Named assumptions/open-questions section with owner + resolution trigger |
| P2-4 | Crosswalk restates canonical rules | **Accepted.** "This runbook owns no rules" declaration added; notes are pointers |
| P2-5 | Checked-in repository map stale | **Accepted — also predated this plan.** `docs/implementation/02-repository-map.md` updated with the probes runbook, crosswalk, coalescing state file, and all three skills |

## 8. Out of Scope

- Vendoring or modifying external suites; per-repo installation of them
- A gstack-style interactive review persona (promotion-tier evidence may
  justify one later, per [DOM-14])
- Propagation to sibling repos (rides with the coalescing propagation)
