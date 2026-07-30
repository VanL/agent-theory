# Program Theory and Module Theory in the Hub

Status: active — retrospective
Class: 3+P — changes the required read order, the scaffold renderer, and
introduces a concept six consumers will copy; process-material, hence +P:
independent review before completion. Hardening: N/A by trigger (docs,
a skill, and create-time scaffold text), but the propagation slice is
boundary-crossing and inherits `propagate-guidance` §4 discipline.

## 0. Why this plan is dated after most of its work

The change began as a documentation edit and was executed as one. It
stopped being a documentation edit at the point where it changed the
required read order, changed what `bin/bootstrap-agent-theory` renders
into every new consumer, and named a concept that other repositories are
expected to adopt. No plan existed at that point, and none was written
until the work was largely built.

Two consequences, stated plainly rather than papered over:

- This plan cannot have constrained what was built. A retrospective plan
  written as though it were prospective is the ceremony
  `[AT-THEORY-7]`'s admission test rejects. It is not offered as a
  governance record for the slices already landed.
- It is still **active**, not completed, and therefore does have forward
  force. Nothing here is committed, no consumer has received any of it,
  no independent review has run, and the spec question in §5 is open.
  The remaining slices are genuinely ahead.

The reclassification trigger is recorded as a lesson, because it is
checkable rather than a matter of judgment: *a task that starts as a doc
edit reclassifies upward the moment it changes read order, changes a
renderer, or names a concept other repositories will copy.*

## 1. Origin

Two independent sources, which is why this is a concept and not a
one-repo preference:

1. **simplebroker** invented `[DOM-16]` (Program Theory and Negative
   Knowledge) and the product-section registry, extending `[DOM-4]`'s
   traceability chain with `program theory` at the head.
2. The owner observed that a recurring pre-design practice — asking "is
   this *simplebroker*ness / *weft*ness / *taut*ness?" against README
   and specs — was orientation around a theory that had no artifact.
   The practice was already load-bearing; only the name was missing.

The second source is the reason the first generalized. Per `[AT-THEORY-7]`
"What earns a place here", the admission test is *can you point at the
practice it names?* — and here the practice predates the name by months.
`mm/cms/ARCHITECTURE.md` (2025) predates it by over a year.

## 2. What landed (uncommitted at time of writing)

- `docs/program-theory.md` (new, untracked) — the hub's own account,
  `[AT-THEORY-0]`–`[AT-THEORY-9]`, including `[AT-THEORY-2.1]` module
  theory and the consumer-replacement preamble.
- `skills/crystallize-program-theory/SKILL.md` (new, untracked) — the
  interview that produces one.
- `AGENTS.md` — program theory becomes step 1 of the required read
  order; module theory gets an entry/no-bulk/no-preload rule.
- `docs/agent-context/README.md`, `context.index.yaml` — read order and
  document roles updated to match.
- `bin/bootstrap-agent-theory` — renders a `Status: Stub` program-theory
  file into new consumers, pointing at the crystallize skill and the
  `[AT-THEORY-8]` question set.
- `README.md`, `docs/README.md`, `docs/specs/00-specs-index.md`,
  `docs/implementation/01`, `02`, `skills/README.md` — orientation and
  map updates.

## 3. Rejected alternatives

This section is the reason the plan is worth writing. The
`[AT-THEORY-*]` text records what was concluded; nothing in the
repository records what was turned down, and those decisions were made
in conversation.

- `[ALT-1]` **Program theory as a new tier in the decision hierarchy.**
  Rejected: it is the frame within which the tiers are read, not an
  authority competing with them. A tier would make it a second
  constitution and invite agents to cite theory against a spec.
  *Reconsider when* two module theories contradict each other and no
  existing tier resolves the conflict.
- `[ALT-2]` **A `theory-check` executable gate** scanning the ecosystem
  and reporting which falsifiers are firing. Rejected on two counts:
  category error — `[DOM-12]` governs *obligations*, while falsifiers
  are epistemic commitments with no obligation to fire; and shape — it
  would be a dashboard, and this corpus consistently chooses tripwires
  over dashboards. It also failed its own admission test: invented from
  analogy, with no practice behind it. *Reconsider when* someone can
  name what they would do differently on a red result.
- `[ALT-3]` **Bulking local depth into `docs/program-theory.md`.**
  Rejected for `MODULE-THEORY.md` next to the code
  (`[AT-THEORY-2.1]`). Progressive disclosure is the whole point:
  apex theory stays short and universally loaded, depth stays local and
  loaded on entry.
- `[ALT-4]` **An "absent state" falsifier** for repos with no theory.
  Retracted: absence is only addressable by agent- or human-mediated
  propagation, so a falsifier watching for it has no action attached.
  The falsifiers were already correctly scoped to *misuse*.
- `[ALT-5]` **An "evidence that this works" section in `README.md`.**
  Rejected: comparative efficacy is not agent-theory. Now a coded
  non-goal in `[AT-THEORY-5]` — the discipline lives in the repository,
  arguments for it live in external writing that cites it. The two age
  on different clocks, and a repository that argues for itself invites
  evaluation of the argument instead of use of the method.
- `[ALT-6]` **Restating surprise-as-collapse-signal in `[AT-THEORY-6]`.**
  Dropped as duplication: `[AT-THEORY-4]` principle 2 already carries
  it, including the non-obvious half (process failures count as theory
  or transfer failures, not only as agent sloppiness).

## 4. Falsifier observables added

`[AT-THEORY-6]` had named falsifiers with no way to tell whether they
were firing. Two now have observables, chosen because both are readable
from material that already exists:

- **Process tower** → *promotion lag*: elapsed time from a behavior
  shipping to a coded clause with a firing gate that owns it. Growing
  lag while the process surface advances is the falsifier firing;
  measurable from git dates without new tooling.
- **False possession** → four probes, weakest to strongest deniability:
  predict the bug class before the agent reports it; design a boundary
  without reopening the transcript; a week away leaves the model intact;
  and *betrayed by an invariant I know* vs *surprised by a system I
  don't own*.

**Module sprawl** was retriggered on divergence rather than precedence:
local theory before apex theory is the healthy order, so the falsifier
now watches for module theories answering the same question differently
or carrying unreconciled product-scope claims.

## 5. Open decision: spec status in the hub

The hub currently carries program theory with **no `[DOM-*]` clause** —
it lives in `docs/program-theory.md` and the `AGENTS.md` read order,
while simplebroker has promoted it to `[DOM-16]` with an extended
`[DOM-4]` chain. That asymmetry is a decision, not an oversight, and it
is the owner's:

- **Promote `[DOM-16]` into the hub spec** — makes program theory an
  obligation with a traceability chain, and gives propagation something
  to cite. Costs: the hub takes on a clause it must then hold every
  consumer to, including repos where a stub is the honest state.
- **Leave it hub-prose** — theory stays a frame rather than an
  obligation, consistent with `[ALT-1]`. Costs: `[DOM-4]`'s chain keeps
  the hole this plan half-closes, and consumers copy a concept with no
  spec anchor.

Recommendation: leave it hub-prose until a second consumer independently
promotes it (the `[DOM-14]` fold-up threshold — two independent
lineages). simplebroker is currently lineage one.

## 6. Remaining slices

1. Commit the current tree as one landing (theory + skill + read order +
   scaffold + maps), so there is a single retrieval cue.
2. Independent review per +P: scoped, different family, §4a-form brief.
3. Propagation wave to the six consumers per `propagate-guidance` §4,
   with the stub-rendering path exercised on a scratch scaffold first.
4. Owner call on §5.

## 7. Verification

- `bin/check-doc-paths` exits 0 on the tree and with `--scaffold`
  (the stub renderer's citations must resolve in a fresh consumer).
- `bin/check-dom15-fixtures` and `bin/coalesce-check` stay green.
- Cross-reference check: `[AT-THEORY-*]` citations resolve to existing
  sections (one defect of this class was found and fixed — line 28 cited
  `[AT-THEORY-9]` for the question set, which lives at `[AT-THEORY-8]`).
- Read-order consistency: `AGENTS.md`, `docs/agent-context/README.md`,
  and `context.index.yaml` `read_order` name the same sequence.

## 8. Out of scope

- Any change to `mm`'s `MODULE-THEORY.md` discoverability (its
  `AGENTS.md` has no route to it) — that is mm's own class-2 fix.
- Retro-editing the closed plans that predate program theory.
- External essay material arguing for the method (`[ALT-5]`).

## 9. Review

Pending. No independent review has run on this change.
