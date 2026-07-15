# Agent-Facing Interfaces Runbook Plan (First Fold-Up)

Status: Active
Class: 3+P (effective 5) — a new runbook that is material to how future
agent-facing surfaces are designed and reviewed. Spec delta: none —
[DOM-12] governs runbook additions; no normative DOM section changes.
Hardening: N/A — no risky trigger (one runbook plus registration rows).

## 1. Goal

Accept the first **role-symmetric fold-up** per [DOM-14]: mm's
agent-API design principles, proposed upward by mm's 2026-07-14 sweep
(recorded in mm `docs/coalescing.md` run log @ `9a8d17d55`), become
`docs/agent-context/runbooks/designing-agent-facing-interfaces.md` —
a reusable standard for designing any surface agents consume (REST/MCP
APIs, CLIs, structured docs).

## 2. Fold-Up Lineage — Honest Accounting (revised per review round 1)

The source is **mm's agent API** (`docs/system_api_design.md`, retired
at mm `9a8d17d55`; shipped as `apps/external_api`, documented in mm's
`implementation/53`): twelve numbered design principles plus a
response `guidance` doctrine, derived from building a production API
for coding agents (2026-03 → 2026-06).

Three different acceptance bases apply, and they are not blurred:

- **Dual-lineage convergence** (satisfies [DOM-14]'s 2-independent
  threshold on its own) for exactly two principles: the mandatory
  actionable `action` field ↔ this repo's required-action rule
  (`principles.md`; discovered in an API and a docs system
  independently), and reference-surfaces-teach ↔ the read-order
  progressive-disclosure model.
- **Single-lineage generalization** for the rest (identity,
  hidden-session-setup, derive-what-is-derivable, fat nodes,
  atomic-writes-with-recovery, trust boundary, compact responses):
  distilled from mm alone. These are accepted not by the convergence
  threshold but by **explicit owner direction** — the user requested
  this synthesis in-session, a tier-1 instruction that outranks
  threshold mechanics. Disclosed here rather than dressed up as
  convergence.
- **Withdrawn convergence claim**: teach-don't-reject vs
  canonicalize-at-boundaries is one lineage, not two — the
  canonical-forms principle entered this repo via mm's pillars in the
  2026-07-02 fold, so both sides share mm ancestry. The runbook cites
  it as a single-lineage validation.

## 3. Invariants

- The runbook is a distillation with a worked example pointer, not a
  spec: it must not restate mm's API mechanics, and every principle
  cites where it was validated or which hub principle owns the
  underlying rule.
- One canonical owner per rule: probe floors stay in
  `adversarial-acceptance-probes.md` and enumerable-contract gating in
  engineering-principles §12 (both cited from a Related Gates section,
  not restated as principles); the required-action rule for guidance
  docs stays in `principles.md` and the `AGENTS.md` agent-usable
  bullet; this runbook owns only the interface-design principles.
- Scaffolded: added to COPIED_FILES (generalizable, like
  `external-skill-suites.md`), the scaffold repo map, this repo's map,
  and `context.index.yaml`.
- Fold-up bookkeeping: hub `docs/coalescing.md` fold-up tier and run
  log record the acceptance with the mm source SHA.

## 4. Tasks

1. Runbook + registrations (COPIED_FILES, scaffold map, repo map,
   context index, plans README row).
2. Pre-landing different-family review (grok, read-only), scoped:
   is each principle genuinely general (not mm-specific)? Is anything
   performative? Is any convergence claim overstated? Full transcript
   captured to a file per the 2026-07-14 lesson.
3. Dispositions, fixes, land; coalescing fold-up record.

## 5. Verification

- Runbook present; each principle carries a validation citation.
- Registration greps: one hit per surface (COPIED_FILES, both maps,
  context index, plans README).
- Review round dispositioned in §6.

## 6. Review Findings and Dispositions

Round 1 (grok, 2026-07-14, read-only, `stopReason: EndTurn`, full
transcript captured to file per the capture lesson): **PASS-WITH-FIXES**
— no P1. All accepted and applied:

| # | Finding | Disposition |
|---|---------|-------------|
| F1 P2 | Principle 12 re-owned enumerable gates + probe floors | Demoted to a "Related Gates (owned elsewhere)" section that cites the owners; runbook is eleven principles |
| F2 P2 | Concurrent merge overstated as universal (forces single-writer CLIs) | Principle 9 split: atomicity + recovery path always; merge machinery gated on multi-writer surfaces |
| F3 P2 | Independence claimed for 12 principles held for ~2; teach-don't-reject convergence circular (shared mm ancestry); threshold met by counting hub doctrine as second incident | §2 rewritten as honest lineage accounting: dual-lineage for two principles, single-lineage-by-owner-direction for the rest (disclosed), teach-don't-reject claim withdrawn; coalescing rows aligned |
| F4 P2 | Validation cites missing on principles 3, 6, 7 | Added (mm principle 1/invisible walls; mm stateless routing; mm normalization guidance + eng-principles §2) |
| F5 P2 | Hub `agent-context/README.md` Runbooks list not updated (scaffolded file) | Bullet added |
| F6 P2 | Principle 6 fought legitimate CLI ambient state | Reworded: ban *hidden session setup*; inspectable, documented ambient context is fine |
| F7 P3 | Wrong owner cite ([DOM-2]) for required-action | Fixed → `principles.md` + AGENTS.md bullet |
| F8 P3 | "eleven" mm principles; source has twelve | Fixed |
| F9 P3 | "state hash" mm-shaped | → "freshness token (hash, ETag, version id)" |
| F10 P3 | Scaffold repo-map omits adversarial-acceptance-probes (pre-existing) | Out of scope here; noted for a follow-up fix |

Reviewer endorsements: mm-specific principles correctly cut
(search-first, facet taxonomy, real-UUIDs); principle 7's
fix-forward distinction; principle 8 as the interface form of
required-action without stealing the doc rule. Round-2: fixes are
scoped retargets/rewrites verified by grep; a full re-round waived and
disclosed.

## 7. Out of Scope

- Propagating the runbook to consumers (arrives with the next wave)
- Amending the [DOM-14] "(for the guidance repo)" boundary wording —
  now unblocked by this first real fold-up, but a separate class-5
  clarification decision
- Any changes to mm
