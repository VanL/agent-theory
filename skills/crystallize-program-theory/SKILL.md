# Crystallize Program Theory

## Purpose

Interview the product owner relentlessly until a theory file can be written:

- **Product theory** — `docs/program-theory.md` (apex shared language), or
- **Module theory** — the **concrete extension** of that model for one owning
  unit (typical path: `<module>/MODULE-THEORY.md`).

Module theory is not a lesser document. It is how the model grows when product
theory would become too long for general entry. See hub
`docs/program-theory.md` [AT-THEORY-2.1].

The result is a transfer surface for agents and humans—not a requirements dump
and not a copy of the agent-theory hub's own theory.

Inspired by interview-style “grill” workflows: one decision at a time, owner
owns the answers, environment facts are looked up rather than asked.

## When To Use

- A consumer repo still has the bootstrap **program-theory stub** (product).
- Product identity is only in chat (“X-ness”) or a long README residual.
- Agents repeatedly propose category errors or re-litigate non-goals.
- **Extending the model:** a subsystem has its own generative rule, ownership
  boundaries, or non-goals; putting them in product theory would bloat general
  entry—write **module theory** instead.
- Before class-5 identity work without a written conceptual account.

## When Not To Use

- Editing the **hub's** theory of agent-theory itself (edit
  `docs/program-theory.md` in this repository under normal review).
- Pure process changes with no product-identity impact.
- Writing exact behavioral contracts (use specs / writing-specs runbook).

## Governing References

- Hub meta-theory: `docs/program-theory.md` [AT-THEORY-0]–[AT-THEORY-8]
- Operating model: `docs/specs/01-development-documentation-operating-model.md`
- Spec writing: `docs/agent-context/runbooks/writing-specs.md`

## Read First

1. Existing `docs/program-theory.md` (hub account, stub, or draft).
2. Product entry (README, agent kernel if any, product-context if any).
3. Any module path the user named for subsystem theory.
4. Recent plans or lessons that show identity friction.

## Blast Radius

- Creates or replaces `docs/program-theory.md` (product) or a module
  `MODULE-THEORY.md` / agreed path.
- May require AGENTS.md / `context.index.yaml` read-order updates so theory
  loads at the right scope.
- Does **not** silently change product specs; identity changes may imply
  later class-5 contract work.

## Workflow

### 1. Frame

State that:

- Program theory is Naur-style working understanding externalized as a
  **current account**.
- Possession stays practical; the file is a transfer surface.
- Hub agent-theory text must not stand as product identity.
- **Module theory is how we extend the product model** when depth is local
  ([AT-THEORY-2.1])—not optional color commentary.
- You will ask **one question at a time**, give a **recommended answer**
  when useful, and wait for the owner.

Decide **scope up front** with the owner: product apex, module extension, or
both (thin product + module). Do not draft the full document until shared
understanding on the spine—or they explicitly ask for a draft from answers so far.

### 2. Interview (one question at a time)

Use the spine in hub `docs/program-theory.md` [AT-THEORY-8]. For each item:

1. Ask the question.
2. Offer a short recommended direction grounded in repo evidence when possible.
3. Wait for the owner's decision.
4. Record the answer; note open dependencies.
5. Only then proceed to the next question.

If a **fact** is in the repo, look it up. **Decisions** stay with the owner.

Walk branches: if non-goals depend on topology ownership, resolve topology
before finalizing non-goals.

### 3. Choose extension shape

| Situation | Action |
|-----------|--------|
| No product theory yet | Crystallize **product** `docs/program-theory.md` first |
| Product theory exists; one module needs deep identity | **Extend** with module theory; do not bulk product theory |
| Answers mix product-wide and local depth | Split: thin product apex + module file(s) |
| Content is exact rules only | Stop; write or update a **contract** (spec/fixture), not theory |

If extending via module theory, require: ownership table, generative model or
equivalent, local non-goals, required action on entry, “no sibling module
theory required,” and promotion path for any product-scope ALT parked there.

### 4. Draft

**Product** — write `docs/program-theory.md` with at least:

- Status / Owner / Boundary / Verification / Required action
- What program theory means (short; link Naur)
- Purpose and desired feel; whole-program mental model
- Core concepts and ownership; principles; non-goals; falsifiers
- How the model is extended (pointer to module theory convention)
- Revisions/ALT if decided; related contracts

**Module** — write `<module>/MODULE-THEORY.md` (or agreed path) with at least:

- Status / Owner / Boundary / Verification / Required action (“read on entry
  to … before changing …”)
- Specializes: product program theory (link)
- What this document is / is not (contracts vs theory)
- Ownership table (owner / consumer / propagator)
- What the module owns; what it is not
- Generative model or design consequences
- Tensions and falsifiers; REV/ALT records
- Related contracts; promotion notes for product-scope items

Use stable section codes if the repo already uses them (`[THEORY-n]`,
`[MODULE-n]`, etc.).

### 5. Wire entry (if missing)

- **Product:** theory early in `context.index.yaml` `read_order` for
  product-scope repository work.
- **Module:** document entry in product theory and/or AGENTS (“when touching
  `path/…`, read `…/MODULE-THEORY.md`”). **Do not** put every module theory
  on global session start.

Do not force full process read order onto product-use-only paths.

### 6. On refuse or revise — write a decision record

If the interview **refuses or defers** a competent proposal, or **changes** the
working model, append a filled ALT or REV using the field shape in hub
`docs/program-theory.md` [AT-THEORY-7.1] (same text as the product theory stub
appendix). Do this **when it happens**, not as a quota of empty records.

Do not create empty `[ALT-001]` placeholders or decision-case directories.

### 7. Confirm

Ask the owner to test possession:

- Place one hypothetical feature.
- Refuse one category error.
- Name one surprise that would revise the theory.

Revise the draft until they confirm.

## Decision record templates

### ALT (rejected / deferred / …)

```markdown
### [ALT-<SCOPE>-<NNN>] Short title

Disposition: rejected | deferred | adopted | superseded | invalidated
Owner: <decision owner>
Governs: <theory section, module theory, or contract reference>
Source record: none | <plan path> | <commit or issue>
Candidate: <what was proposed>
Why plausible: <steelman>
Evidence:
- contemporaneous | owner-recalled | inferred | unknown: <source>
Reason: <why this disposition>
Current consequence: <what work must do now>
Reconsider when: <observable condition — not vibes>
Promoted to: none | <id if moved upstairs or into a contract>
```

### REV (theory change)

```markdown
### [REV-<SCOPE>-<NNN>] Short title

Current account: <revised theory — put current first>
Supersedes: <short prior account; do not let it compete with current>
Pressure: <what made the prior account inadequate>
Evidence:
- contemporaneous | owner-recalled | inferred | unknown: <source>
```

## Output Standard

- Written theory file at the agreed path.
- Explicit non-goals and ownership table.
- Entry-order note or patch so the file is loadable by agents.
- Any **real** ALT/REV from the interview filled in full; zero empty slots.
- List of follow-ups (spec promotions, parked ALTs) without implementing them
  unless asked.

## Anti-patterns

- Copying the hub's agent-theory program-theory into a product repo as-is.
- Stuffing module depth into product theory “so agents see it,” instead of
  **extending** with module theory and entry wiring.
- Writing module theory that requires three sibling theories to place work
  (broken ownership table).
- Turning the interview into a full architecture dump or API catalog.
- Asking multiple independent questions in one turn.
- Acting on implementation before shared understanding is confirmed.
- Treating the written file as proof of possession without the placement/refusal
  test.
- Pre-creating empty ALT/REV records or decision directories “for later.”

## Maintenance Notes

- Keep ALT/REV field lists in sync with hub [AT-THEORY-7.1] and the bootstrap
  stub appendix.
- Update the spine when hub [AT-THEORY-8] changes.
- If interviews always need the same extra domain questions, promote them into
  this skill.
- If consumers keep shipping without replacing the stub, strengthen bootstrap
  messaging and AGENTS required-action language.
