# Register-Conditioning Theory Revision Plan

Date: 2026-08-06
Status: draft — round-1 independent semantic review complete
(ADOPT-WITH-EDITS; all edits applied); amended 2026-08-07 per OD-3 of
`docs/plans/2026-08-07-simplebroker-backport-wave-plan.md` (owner
confirmed); amendment independently reviewed 2026-08-07
(ADOPT-WITH-EDITS, both edits applied); awaiting owner adoption of the
full delta
Type: spec-authoring / theory revision (no code; three text deltas)

## Goal

Externalize one position the corpus already practices but does not
name: guidance artifacts carry a working register in addition to their
propositions, so composing the always-loaded surfaces — including
their citations — is a capability-environment decision, not a style
choice. Land it as a theory revision record, one [AT-THEORY-6]
falsifier, and one line in the crystallize skill's drafting guidance.
Nothing else from the source dialogue is proposed (see Withheld,
below).

## Source Documents

- `docs/program-theory.md` [AT-THEORY-2] (the mental model this
  extends), [AT-THEORY-5] (the efficacy non-goal this must not
  violate), [AT-THEORY-7] (admission test: point at the practice).
- `skills/crystallize-program-theory/SKILL.md` (drafting guidance the
  operational line joins).
- Practice named: the owner's deliberate inclusion of the
  Naur/Knuth/Ronacher references in this repository's and consumers'
  theory files — confirmed by the owner as a conscious
  register-conditioning decision, not decoration; the corpus house
  style (dense, spec-coded prose in always-loaded surfaces); and the
  simplebroker register-symmetry evidence recorded in this
  repository's `docs/lessons.md` (2026-08-06 entries: well-formed ≠
  verified; register symmetry).
- Owner-recalled: the 2026-08-06 owner dialogue. The dialogue proposed
  a causal mechanism (register evokes matching-capability output; the
  corpus makes the owner's engagement level ambient); round-1 review
  classified that mechanism as ahead of practice, and only the
  position — register as part of the capability environment —
  survives into the delta. The mechanism remains source material for
  external writing, not a claim of this plan.

## Baseline

- Hub working tree at `4acbad1` plus the owner's uncommitted
  in-flight edits (dirty tree; this plan and today's lessons entries
  are among them). The delta below targets `docs/program-theory.md`
  [AT-THEORY-9] (new revision record) and the crystallize skill.

## Proposed Delta 1 — `docs/program-theory.md`, append to
[AT-THEORY-9] (reviewer-edited text, round 1)

> ### [REV-AT-003] The corpus carries register as well as information (2026-08-06)
>
> Current account: Guidance artifacts communicate propositions and also
> establish a working register: the vocabulary, distinctions, and
> intellectual lineages through which agents frame the work. The hub
> therefore treats composition of always-loaded surfaces as a
> capability-environment decision, not merely a style choice. Citations
> can participate in that environment when they are accurately
> represented and contribute concepts, distinctions, or refusals the
> account actually uses. The Naur, Knuth, and Ronacher references in
> this file are current examples. Register remains non-evidentiary:
> fluent form can camouflage error, so correctness continues to depend
> on executable gates and independent review.
> Supersedes: The prior account treated the corpus primarily as an
> informational and ownership surface while leaving the role of
> register and citation selection unnamed.
> Pressure: The owner's deliberate use of the Naur, Knuth, and Ronacher
> lineage as part of the hub's conceptual frame, together with the
> simplebroker pre-release review cycle in which the same hardening
> register carried both sound and unsound proposals.
> Evidence:
> - contemporaneous: this file's intellectual-lineage table and
>   `docs/lessons.md` 2026-08-06 entries on well-formed plans and
>   register symmetry (same-worktree records of the same dialogue —
>   contemporaneous, not independent validation)
> - owner-recalled: citation selection was intended partly to establish
>   the conceptual register, confirmed 2026-08-06

## Proposed Delta 1b — `docs/program-theory.md`, new [AT-THEORY-6]
falsifier bullet (reviewer-relocated and made operational)

> - **Register without transfer:** If predeclared, blinded paired
>   probes across the currently supported model mix show no repeatable
>   change in framing or correct concept use when register changes
>   while propositions are held constant, narrow the account to the
>   informational function. Apply the same test to citation anchors by
>   removing citation and lineage cues while preserving the
>   propositions attributed to them; if no material effect survives the
>   predeclared threshold, retain those citations only for provenance.

## Proposed Delta 2 — `skills/crystallize-program-theory/SKILL.md`,
drafting-guidance line (reviewer-edited text)

> Choose references on two tests: **accurately represented** and
> **load-bearing**. A load-bearing reference contributes a concept,
> distinction, refusal, or vocabulary the theory actually uses. Make
> that contribution explicit where it would otherwise be unclear; omit
> ornamental citations. Treat any register effect as a drafting
> hypothesis, never as evidence that the theory or its outputs are
> correct ([REV-AT-003]).

## Withheld from this proposal (deliberately)

- Feel-report epistemics (tiered validity of agent introspection):
  one dialogue, no repeated practice — fails [AT-THEORY-7]'s
  admission test today.
- The strong interrogator-cap claim: the most model-generation-
  sensitive assertion in the source dialogue; belongs in external
  writing per [AT-THEORY-5] if anywhere.
- Any efficacy framing: the round-1 draft itself smuggled causal
  performance claims ("shifts which region of capability is evoked",
  "raises output quality") despite this section's assertion otherwise;
  the reviewer-edited text above removes them, retaining position and
  falsifier only. The mechanism claims stay in the source dialogue and
  any external writing.

## Amendment (2026-08-07 — OD-3 of the backport wave, owner-confirmed)

Two additions to Delta 1, routed through a fresh independent semantic
review before adoption. Round-1 review of the backport plan classified
an attributed favorable impression as an efficacy claim by type;
round-2 confirmed even directional attribution is excluded. The
wording below is therefore content-free about direction; the
observation's content lives in the backport plan's execution log and
any external writing, never in current-account theory.

**Amendment A — add as a second sentence within [REV-AT-003] Pressure
(amendment-review edit AM-2 applied — a complete sentence, not an
append fragment):**

> The owner's motivating impression about register effects was a
> further pressure; its content is recorded in the backport plan's
> execution log
> (`docs/plans/2026-08-07-simplebroker-backport-wave-plan.md`) and is
> disqualified as evidence by this revision.

**Amendment B — append to [REV-AT-003] Current account (experiment
status; amendment-review edit AM-1 applied — hypothesis narrowed to
the falsifier's measured dimensions, evidence deficit stated
directly):**

> This corpus is, in part, an experiment in shaping the capability
> environment agents draw on. The working hypothesis is that register
> and citation composition affect output framing or correct concept
> use. No predeclared, blinded paired probe across the currently
> supported model mix has run; the motivating observations are
> confounded by fluency and do not support that hypothesis. The
> account stays narrow until the register falsifier in [AT-THEORY-6]
> has been exercised; the falsifier is the standing invitation to
> test it.

**Amendment review (2026-08-07, codex, scoped to this section):**
per-question verdicts — [AT-THEORY-5] PASS (no favorable-quality
assertion); [AT-THEORY-7]/falsifier consistency and REV format
ADOPT-WITH-EDITS. Findings AM-1 (P2, hypothesis broader than Delta
1b's testable dimensions; confound framed as weak support) and AM-2
(P3, append produced a sentence fragment): both accepted; the
reviewer's exact replacement texts are the texts above. Verdict:
**ADOPT-WITH-EDITS — edits applied.**

## Review Loop

- Independent semantic reviewer (different family; Codex), stance:
  (1) does the delta pass [AT-THEORY-7]'s admission test — is the
  named practice real and sufficient, or is this dialogue-driven
  theorizing ahead of practice? (2) does it violate [AT-THEORY-5]'s
  efficacy non-goal anywhere? (3) is [REV-AT-003] format-conformant
  with [REV-AT-001/002] (current account / supersedes / pressure /
  evidence, falsifier placement)? (4) is the recursive-reference
  claim sound or self-congratulatory? (5) does the skill line belong
  in the skill rather than the theory file (second-operating-manual
  falsifier)? (6) is the falsifier actually falsifiable? Explicit
  verdict: adopt, adopt-with-edits, or reject.
- Owner adoption decision after review; the delta is not landed by
  this plan.

## Out of Scope

- Landing either delta (owner + review gate).
- Any change to [AT-THEORY-1..5, 7, 8] body text, the primer, DOM
  specs, or consumer repositories. ([AT-THEORY-6] gains exactly one
  falsifier bullet — Delta 1b — per the reviewer's placement ruling;
  the round-1 exclusion of all of 1..8 was format-incorrect.)
- The withheld items above.

## Independent Review (Round 1, 2026-08-06)

**Verdict: ADOPT-WITH-EDITS** (Codex, read-only semantic pass against
the hub corpus, worktree diff, and git history). All exact edits
applied above. Findings and dispositions:

1. Admission test: passes for the narrow practice (deliberate lineage
   citation, curated register); the broad causal mechanism ("elevated
   register activates higher capability") is theorizing ahead of
   practice — the simplebroker evidence establishes register symmetry
   and camouflage, not capability activation. **Accepted:** mechanism
   claims removed; the record names the practice and the
   capability-environment position only.
2. [AT-THEORY-5]: round-1 draft smuggled efficacy claims in four
   quoted phrases. **Accepted:** all four removed.
3. Format: standalone `Falsifier:` field non-conformant with
   [REV-AT-001/002] and the crystallize template; falsifiers belong in
   [AT-THEORY-6]. **Accepted:** Delta 1b relocates it; Out of Scope
   amended. `Supersedes` overstated the prior doctrine ("solely
   propositional") — **accepted:** now describes an omission.
4. Recursive-reference sentence ("a reference that exemplifies the
   rule it justifies is the right kind of reference") rejected as
   circular and self-congratulatory. **Accepted with a note for the
   owner:** the replacement keeps the fact (the three citations are
   conscious, inspectable instances) while dropping the universal
   claim; the owner valued the recursive framing and may wish to
   overrule — that is an adoption-time call, recorded here rather than
   silently conceded.
5. Placement: skill owns the operational test; theory names position
   plus examples. **Accepted:** the twofold test moved out of the
   revision record into Delta 2 only.
6. Falsifier unfalsifiable as drafted (future-models deferral,
   universal negative, undefined measures). **Accepted:** replaced
   with the reviewer's present-tense, predeclared-threshold version.
7. Drafting defects ("every session", "summon a tradition", "true" as
   a test name, model-psychology phrasing). **Accepted:** all removed;
   "true" → "accurately represented".

Owner adoption remains the gate; nothing is landed by this plan.
