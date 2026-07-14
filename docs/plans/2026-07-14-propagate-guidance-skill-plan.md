# Propagate-Guidance Skill Plan

Status: Active — promoted 2026-07-14 after two grok rounds (round 1
blocked on F1/F2 completeness; round 2 PASS including the
could-you-run-mm gate)
Class: 3+P (effective 5) — a new reusable skill that is material to how
future propagation work is done. Spec delta: none required — [DOM-12]
governs skills; the propagation workflow operationalizes existing
guidance and creates no new normative contract. Hardening: N/A — no
risky trigger (the skill documents a docs workflow).

## 1. Goal

Harvest the four-landing propagation workflow (taut `c09e95e`,
backstitch `9ddb4d6`, engram `f92fa82`, weft `1e2e16d`, all 2026-07-14)
into a hub-native skill before it decays into session memory. Promotion
evidence per the skill-lifecycle rule and the crosswalk's citation
standard: four runs in one day, refined each time, with eight scoped
review rounds citing its process defects.

## 2. Placement Decision (user-decided 2026-07-14)

**Hub-native; NOT in COPIED_FILES.** Rationale: propagation flows
guidance-repo → consumers; consumers have no outbound role (fold-up is
the coalescing skill's guidance-repo-only tier, a different motion).
Precedent: `bin/bootstrap-agent-guidance` — the fresh-install
counterpart — is likewise not copied. Keeping hub-only surfaces out of
COPIED_FILES also eliminates the "residual guidance-repo wording"
review-noise class that the backstitch and engram adaptation reviews
both flagged.

## 3. Invariants

- The skill encodes the *hardened* workflow, including every defect the
  four landings hit: string-anchor splices, mid-script death with
  silent omissions, blanket-replace garbling, foreign-WIP staging
  traps, false-positive content greps, script tails that commit after a
  failed check.
- One canonical owner: the staging-safety and cd-persistence rules stay
  in `docs/lessons.md`; the skill operationalizes and cites them.
- Two canonical-text improvements ride along: the name-not-bare-number
  citation rule for portable guidance (owned by this skill), and an
  adopter-facing comment in `bin/check-dom15-fixtures` stating that
  negative-fact markers are repo-adapted by design.
- No DOM spec change: [DOM-14]/[DOM-15] survived four adaptations with
  zero semantic amendments — that validation is recorded, not
  disturbed.

## 3a. Proposed Spec Delta

None. Rationale: [DOM-12] governs skills; the propagation workflow
operationalizes existing guidance and lessons without creating a new
normative contract, and [DOM-14]/[DOM-15] deliberately receive no
amendment after surviving four adaptations unchanged. Promotion
strategy: N/A.

## 4. Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## 5. Tasks

1. `skills/propagate-guidance/SKILL.md` (Draft) + this plan +
   status-index row. Done: files exist, template order.
2. Pre-landing review (+P, different family), scoped: could you run a
   fifth propagation (mm) from this skill alone? Does it encode all
   eight review rounds' findings? Anything performative? Blocker for 3.
3. Promotion: skill status → Active; canonical checker comment added;
   repo-map row (this repo's map only — not the scaffold renderer,
   per §2). mm's propagation becomes the first consumer.

## 6. Verification

- Skill-shape: template section order (inspection).
- The skill's workflow steps each cite the landing or review round that
  produced them (spot-checkable against the four propagation plans).
- backstitch self-corpus check 0/0/0 after landing.

## 7. Review Findings and Dispositions

Round 1 (grok, 2026-07-14): **BLOCKED** — F1/F2 P1 (completeness
against the plan's own could-you-run-mm gate), F3–F7 P2. All accepted:
F1 wave-inventory/payload-checklist step 0 added (the recovery source
and completeness gate the four landings used but never wrote down);
F2 foreign-code-scheme survey axis + explicit keep/dual-cite/name-map
decision with a ban on silent renumbering; F3 read-first made
hub-self-sufficient; F4 minimal command shapes inlined; F5 state-file
derivation + not-derivable path made mandatory pre-sweep; F6 the
review-rounds claim replaced with the defect→landing map; F7 this
named empty delta. Endorsed: process-defect honesty, hub-native
placement, spec-delta-none substance. Round 2 (grok, scoped): all
seven fixes verified OK; gate question re-answered PASS — mm runnable
from the skill alone, with the receiving repo's AGENTS.md/gates as the
stated guest obligations.

## 8. Out of Scope

- Adding the skill to COPIED_FILES or the scaffold (decided against, §2)
- The mm propagation itself
- Automating transplants beyond documented script patterns
