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

Additive guidance; review after landing is acceptable. Reviewer stance:
does the crosswalk resolve precedence unambiguously for an agent that has
both suites installed? Are the two harvested skills self-sufficient
without the external suite present? Dispositions recorded here.

## 8. Out of Scope

- Vendoring or modifying external suites; per-repo installation of them
- A gstack-style interactive review persona (promotion-tier evidence may
  justify one later, per [DOM-14])
- Propagation to sibling repos (rides with the coalescing propagation)
