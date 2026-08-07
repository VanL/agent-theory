# Commit-Subject Principle Promotion Plan

Date: 2026-08-07
Status: draft — promotion candidate awaiting independent semantic
review, then owner adoption
Type: guidance promotion (lesson → engineering-principles §16; no code)

## Goal

Promote the commit-subjects lesson to engineering-principles §16, its
pre-declared threshold having fired: the 2026-07-17 lesson recorded two
lineages and named "candidate for engineering-principles once cited
from a third context"; the third context occurred 2026-08-07 (weft's
lint-expansion commit carrying four reviewed correctness fixes,
including a wire-protocol arity change, repaired the same day by
retroactive CHANGELOG disclosure). The promoted text is floor-honest
per the self-application lesson: the owner reports uneven
authoring-time compliance, so the enforceable floor is review-time
detection plus a normalized repair path — not authoring-time
perfection.

## Source Documents

- `docs/agent-context/engineering-principles.md` (target; §16 inserted
  before "Warning Signs"; §14's floors-not-ideals framing is the
  pattern followed).
- `docs/lessons.md` 2026-07-17 commit-subjects entry (the promoting
  lesson; its trailing note updates in the same change).
- 2026-08-06 lesson "a doctrine that has not been self-applied drifts
  first… write each new doctrine with its floor named" (the floor
  requirement this text satisfies).
- Third-lineage evidence: weft `bb6e4776` and its 2026-08-07
  retroactive CHANGELOG disclosure entries (weft repo, branch
  `codex/ruff-lint-expansion-plan`); owner compliance self-report,
  2026-08-07 dialogue.

## Baseline

- Hub working tree (dirty; owner in-flight edits). Target file
  section map verified: §15 ends before `## Warning Signs`.

## Proposed Delta 1 — `docs/agent-context/engineering-principles.md`,
new §16 before "Warning Signs" (reviewer-edited text)

> ## 16. Commit Subjects Name the Largest-Impact Change — With a Repair Path
>
> The commit log is a review surface, and a subject line is a claim
> about what the diff contains. A contract, protocol, authority, or
> behavior change riding under a subject named for something else hides
> the highest-impact hunk from the people who use the log to decide
> what to inspect.
>
> Rules:
>
> - Name the largest-impact change, not the largest-volume change. A
>   one-line protocol field outranks seven thousand lines of tests.
> - A subject framed solely as `refactor:`, `lint:`, `cleanup:`, or
>   `deps:` must not conceal a higher-impact semantic change. Qualify
>   the subject with that change when it dominates review or
>   operational risk.
> - Reviewed-elsewhere is not disclosed-here: a change documented in a
>   plan or registry row still owes the log its true subject, because
>   the log is read by people who will never open the plan.
> - **The verification floor is subject-versus-diff review plus a
>   durable repair path.** Before landing, independent and completion
>   reviews compare each commit subject with the diff's highest-impact
>   changes. An unpublished mislabeled commit is corrected in place. If
>   a mislabeled commit has already been published, add prompt, durable
>   disclosure in the repository's canonical history or release surface,
>   referencing the commit; do not rewrite published history. Repair
>   restores disclosure but does not make the original subject
>   compliant. Knowing or repeated mislabeling remains a violation and
>   triggers reconsideration of automated enforcement.
>
> Subject accuracy is fallible for humans and agents alike, so the rule
> carries both a review-time verification floor and a recovery path.
> The recovery path does not relax the authoring rule. Provenance:
> `docs/lessons.md`, 2026-07-17 commit-subjects entry.

## Proposed Delta 1b — `docs/agent-context/engineering-principles.md`,
new Warning Signs bullet

> - a refactor, lint, cleanup, or dependency subject contains a
>   higher-impact contract, protocol, authority, architecture, or
>   behavior change

## Proposed Delta 1c — review-loops runbook, standing item
(self-application per the doctrine-floor lesson)

Add to the completed-work review checklist in
`docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md`:

> - Subject-versus-diff: for each commit under review, confirm the
>   subject names the diff's highest-impact change
>   (engineering-principles §16); flag any generic-subject commit
>   carrying contract, protocol, or behavior changes.

## Proposed Delta 2 — `docs/lessons.md`, 2026-07-17 entry trailing note
(reviewer edit 10 applied — per-lineage attribution)

Replace "Two independent lineages; candidate for engineering-principles
once cited from a third context." with:

> Three lineages as of 2026-08-07: the weft dependency-pin case
> supports subject specificity and discoverability; the mm omnibus and
> weft lint-expansion cases support the concealed-semantic-change rule
> (the latter repaired by retroactive CHANGELOG disclosure). Promoted
> to engineering-principles §16 with a subject-versus-diff review floor
> and durable repair path.

## Deliberately excluded

- Any commit-msg hook or CI heuristic gate. A hook cannot judge
  semantic impact; the doctrine-floor lesson permits declared-claim-
  plus-review. **Measurable reconsideration condition (reviewer edit
  9):** reconsider automated enforcement after two further
  post-adoption landed mislabels require retroactive repair, or after
  one undisclosed mislabel passes the standing review check and causes
  a concrete downstream error in review, release notes, or incident
  analysis. Reconsideration means evaluating an enforceable heuristic,
  not presuming a commit-msg hook can judge semantic impact.
- Any change to [DOM-15]'s class-1/2 commit-record requirements — a
  separate decision with its own tradeoffs.
- The owner compliance self-report stays in this plan and the review
  record, not in the always-loaded principle (reviewer edit 5).

## Review Loop

- Independent semantic reviewer (different family), stance: (1) does
  the promotion threshold genuinely fire (three real lineages, not one
  incident recounted thrice)? (2) is the detection-and-repair floor a
  legitimate floor per the doctrine-floor lesson, or a loophole that
  makes the rule unenforceable (attack: does "repair counts as
  compliance" invite deliberate mislabel-then-disclose)? (3) is the
  owner-compliance sentence in Lineage honest self-knowledge or
  self-undermining text that weakens the rule's authority? (4) wording
  defects, overlaps with existing principles (§8 review, Golden Rule
  10 calibration), placement. Explicit verdict: adopt /
  adopt-with-edits / reject.
- Owner adoption after review; nothing lands from this plan directly.

## Independent Review (Round 1, 2026-08-07)

**Verdict: ADOPT-WITH-EDITS** (Codex, read-only semantic pass; all ten
edits applied above). Key dispositions:

1. Threshold fires — three distinct incidents (two repos is fine; two
   weft cases are separate events). Accepted, with edit 10's
   per-lineage attribution: the deps-pin case proves specificity, not
   behavior-preservation claims.
2. The original repair floor was a loophole — "only undisclosed
   mislabeling is the defect" licensed mislabel-then-disclose and
   failed the §14 analogy (floors never redefine violations as
   compliance). **Accepted:** reviewer's formulation adopted verbatim;
   repair restores disclosure, never compliance; knowing/repeated
   mislabeling named a violation.
3. Owner-compliance sentence removed from the always-loaded surface
   (embedded excuse + transient biography); retained here as design
   rationale. Accepted.
4. Categorical `deps:`-claims-preservation assertion was false;
   replaced with the higher-impact-concealment formulation. Accepted.
5. Floor self-applied: Delta 1c wires subject-versus-diff into the
   review runbook (the doctrine-floor lesson's requirement).
   Accepted.
6. Unpublished-correction vs published-repair distinguished; "never a
   history rewrite" narrowed to published history. Accepted.
7. Warning Signs bullet added (Delta 1b). Accepted.
8. Gate reconsideration made measurable. Accepted.
9. Lineage paragraph moved out of the principle; provenance pointer
   retained. Accepted.

Owner adoption remains the gate; nothing lands from this plan
directly.
