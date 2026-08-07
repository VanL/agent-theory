# Program Theory and Module Theory in the Hub

Status: active — repair pass after independent review
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
- It remains **active** for remaining work (propagation, residual hygiene).
  Forward force applies to slices not yet done.

The reclassification trigger is recorded as a lesson: *a task that starts
as a doc edit reclassifies upward the moment it changes read order, changes
a renderer, or names a concept other repositories will copy.*

## 0.1 Process deviation: pre-review landing (honest record)

**Deviation:** Class `3+P` requires independent review before completion /
landing. The theory wave landed on `main` as commit **`4acbad1`**
(*Add program-theory docs*) **before** independent review ran.

**What must not be claimed:** that review occurred before `4acbad1`, or that
the plan constrained that commit.

**What this plan records:**

| Fact | Value |
|------|--------|
| Landed baseline | `4acbad1` on `main` |
| Plan text at land | Still said "uncommitted" / "review pending" (stale transient state frozen as if durable — same class of error the contemporaneous lesson warned against) |
| Independent review | 2026-07-30 external review of the agent-theory tree (findings below) — **after** `4acbad1` |
| Disposition of review | Repair pass in this plan §10; does not rewrite history to imply pre-landing review |

This review can serve as the missing independent review for the wave; the
repository records it honestly rather than backfilling order.

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

## 2. What landed in `4acbad1`

- `docs/program-theory.md` — hub account `[AT-THEORY-0]`–`[AT-THEORY-9]`,
  including `[AT-THEORY-2.1]` module theory and consumer-replacement preamble.
- `skills/crystallize-program-theory/SKILL.md` — interview that produces one.
- `AGENTS.md` — program theory step 1 of required read order; module theory
  entry/no-bulk/no-preload rule.
- `docs/agent-context/README.md`, `context.index.yaml` — read order and roles.
- `bin/bootstrap-agent-theory` — `Status: Stub` program-theory for new consumers.
- `README.md`, maps, specs index orientation.

## 3. Rejected alternatives

- `[ALT-1]` **Program theory as a new tier in the decision hierarchy.**
  Rejected: frame, not competing authority. *Reconsider when* two module
  theories contradict and no existing tier resolves the conflict.
- `[ALT-2]` **A `theory-check` executable gate** for falsifiers. Rejected:
  category error and no practice behind it.
- `[ALT-3]` **Bulking local depth into `docs/program-theory.md`.**
  Rejected for `MODULE-THEORY.md` next to code (`[AT-THEORY-2.1]`).
- `[ALT-4]` **An "absent state" falsifier** for repos with no theory.
  Retracted: no action attached.
- `[ALT-5]` **Comparative efficacy section in README.** Rejected as advocacy.
  **Amended by review finding 7:** factual provenance and adoption links
  *are* allowed in the hub README; comparative claims remain external.
- `[ALT-6]` **Restating surprise-as-collapse-signal in `[AT-THEORY-6]`.**
  Dropped as duplication of `[AT-THEORY-4]` principle 2.
- `[ALT-7]` **Binary choice: new `[DOM-16]` vs leave theory as hub prose only.**
  Rejected as false binary (independent review finding 2). Narrower path:
  name program theory in `[DOM-2]`/`[DOM-3]` as frame, not as a hierarchy tier
  and not as a full simplebroker-style `[DOM-16]` obligation until fold-up.

## 4. Falsifier observables (from first wave)

- **Process tower** → promotion lag.
- **False possession** → four probes (betrayal vs surprise).
- **Module sprawl** → divergence, not precedence.

## 5. Spec status (resolved narrow; full DOM-16 deferred)

**Resolved (repair pass):** amend hub `[DOM-2]` and `[DOM-3]` so the operating
model describes program theory as a distinct artifact role and matches the
required startup order in `AGENTS.md`. State explicitly that theory frames
interpretation and placement but does not override winning contracts; define
`Stub` / `Draft` / `Active` behavior; optional theory alignment on
identity-changing work in `[DOM-4]` only.

**Still deferred:** promoting a full consumer-facing `[DOM-16]` obligation
with an extended mandatory traceability chain for every product repo (the
simplebroker lineage). Reconsider when a second consumer independently
promotes the same obligation (fold-up threshold).

## 6. Remaining slices

1. ~~Commit first wave~~ — done: `4acbad1`.
2. ~~Independent review~~ — done after land (this review); deviation recorded.
3. **Repair pass** (this work) — findings §9 / dispositions §10.
4. Propagation wave to consumers — **blocked until repair pass lands and
   gates are green**; then `propagate-guidance` §4.
5. Owner call on full `[DOM-16]` — still optional/deferred per §5.

## 7. Verification

- `bin/check-doc-paths` exits 0 on the tree and with `--scaffold`.
- `bin/check-dom15-fixtures` and `bin/coalesce-check` stay green.
- Scaffold identity assertion: consumer copies free of forbidden hub-identity
  phrases (`this hub repository`, `what agent-theory is`,
  `conceptual identity of this guidance system`, `hub conceptual identity`).
- Read-order consistency: `AGENTS.md`, `docs/agent-context/README.md`,
  `context.index.yaml`, and `[DOM-3]` name the same sequence.
- CI workflow runs the gates on push/PR.

## 8. Out of scope

- Any change to `mm`'s `MODULE-THEORY.md` discoverability.
- Retro-editing closed plans that predate program theory.
- External essay material arguing for the method (`[ALT-5]` advocacy half).
- Propagation into consumer repositories (after repair lands).

## 9. Independent review (2026-07-30, post-`4acbad1`)

**Verdict (reviewer):** Intellectual direction strong enough to support the
Agent Theory brand. Tree **blocked for propagation and public promotion**
until three internal contradictions fixed. Blockers repairable.

### Blocking findings

| ID | Finding | Disposition |
|----|---------|-------------|
| B1 | Bootstrap copies hub-identity language in entry docs; product `program-theory` says product while surrounding docs say hub | **Fixed:** scope-neutral entry docs; scaffold identity assertion in bootstrap |
| B2 | Mandatory read order contradicts governing DOM (no program theory in taxonomy/startup) | **Fixed:** `[DOM-2]`/`[DOM-3]`/`[DOM-4]` amended as frame, not hierarchy tier (`[ALT-7]`) |
| B3 | Plan asserted uncommitted/review-pending after `4acbad1` landed pre-review | **Fixed:** §0.1 deviation; this section; plan index updated; no backfill of pre-land review |

### Important findings

| ID | Finding | Disposition |
|----|---------|-------------|
| I4 | Theory file becoming second operating manual; templates triplicated | **Fixed:** trim theory to conceptual account; skill owns spine/templates/checklist; short stub |
| I5 | "Before design work" gate implies big design up front | **Fixed:** begin crystallization before *committing* product-scope behavior; Class 5 needs Draft; exploration allowed |
| I6 | README not a public Agent Theory landing page | **Fixed:** discipline vs repository vs slug; failure mode first |
| I7 | No factual provenance/adoption links | **Fixed:** provenance section; Taut/Backstitch/SimpleBroker/Weft; not efficacy claims |
| I8 | Trusted instruction provenance (which revision of guidance is trusted) | **Fixed:** trusted-base rule in decision hierarchy |
| I9 | No CI for executable gates | **Fixed:** `.github/workflows/gates.yml` |

### Priority order executed

1. Scaffold identity contradiction  
2. DOM-2/3 reconcile  
3. Plan/review/deviation record  
4. Stub gate wording  
5. Trim theory / skill ownership / short stub  
6. README rewrite  
7. Provenance  
8. Trusted base + CI  

Propagation remains **after** this repair lands.

## 10. Repair pass file list (this change)

- Scope-neutral: `docs/README.md`, `docs/agent-context/README.md`,
  `docs/specs/00-specs-index.md`
- Spec: `docs/specs/01-development-documentation-operating-model.md` [DOM-2/3/4]
- Trust: `docs/agent-context/decision-hierarchy.md`
- Gate/stub: `AGENTS.md`, bootstrap stub renderer, identity assertion
- Theory trim: `docs/program-theory.md` [REV-AT-002]
- Skill owns ops: `skills/crystallize-program-theory/SKILL.md`
- Public entry: `README.md`
- Maps: `docs/implementation/02-repository-map.md`
- CI: `.github/workflows/gates.yml`
- This plan + `docs/plans/README.md` index row

## 11. Review status

Independent review **received** 2026-07-30 (post-land). Findings §9
incorporated or answered in the repair pass. Pre-landing +P process was
**not** followed for `4acbad1`; deviation is explicit in §0.1.
