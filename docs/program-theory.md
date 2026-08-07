# Agent-Theory Program Theory

Status: Active — first draft
Owner: agent-theory maintainers
Boundary: Conceptual identity and design judgment for **this guidance system**,
not product behavior of any consuming repository.
Verification: Owner and independent semantic review; structural consistency
with `docs/specs/01-development-documentation-operating-model.md` and the
bootstrap surface.
Required action: Read before changing the purpose of the hub, the artifact
graph, progressive-disclosure rules, or bootstrap defaults. Conform or propose
an explicit theory revision.

---

## Consumer repositories — replace this account

**This file is the program theory of *agent-theory* (the guidance hub and
scaffold).** It is **not** a product program theory for application or library
codebases.

When a product or library repository adopts this scaffold:

1. **Do not keep this document as the product's theory.** Replace
   `docs/program-theory.md` with an account of *that* product's problem,
   concepts, ownership, non-goals, and falsifiers.
2. Use `skills/crystallize-program-theory/SKILL.md` to interview the owner
   until a product-specific theory can be written.
3. Keep progressive disclosure: product theory stays short. When a subsystem
   needs its own generative model, non-goals, or ownership table, **extend the
   model with module theory** next to that code ([AT-THEORY-2.1])—do not bulk
   the product file.
4. Until replacement, treat any copied hub theory as **process orientation
   only**, never as authority for product behavior.

The bootstrap installs a **stub** product program-theory for new consumers so
this hub account is not mistaken for product identity. Module theory is not
bootstrapped as a blank file everywhere; it is the **named extension
mechanism** when product theory would otherwise grow unreadable.

---

## What this repository claims about theory [AT-THEORY-0]

The definition — what a program theory *is*, how it differs from a spec, and
why anyone should care — lives in the primer,
`docs/specs/02-agent-theory-and-program-theory.md` [AT-REF-2]. Read that first
if the term is new. This section holds something the primer cannot: the hub's
**positions**, the contestable claims that make this repository the system it
is rather than a neutral account of Naur.

“Theory” here follows Peter Naur's *Programming as Theory Building*
(1985).[^naur] **Possession is practical, not mnemonic** — the primer lists the
four things someone who holds a theory can do; memorizing this file is not one
of them. The fuller working theory is rebuilt from this account together with
the operating-model spec, runbooks, skills, gates, consumer dogfood, and
concrete surprises.

### Intellectual lineage

The right-hand column is the load-bearing one: what this repository **declines**
to take from each source. Those refusals are positions, and they are where the
account could turn out to be wrong.

| Source | What we take | What we do not take |
|--------|----------------|---------------------|
| **Naur (1985)** | Programming as theory-building; docs secondary to possession; modification quality depends on theory; program “death” when theory-holders disperse | That theory can never be externalized usefully; we externalize a *current account* as a transfer surface, not as a complete substitute for possession |
| **Knuth (literate programming)** | Explanation is for human understanding and should stay in contact with executable realization[^knuth] | A single master literate source for everything; we keep separate surfaces for different questions, linked by traceability |
| **Ronacher (2026), “The Tower Keeps Rising”** | Shared language (concepts, boundaries, invariants, ownership, why) is the scarce resource under AI-assisted work; agents remove friction that used to force that language; construction can continue after shared understanding has already collapsed[^ronacher] | That the only response is to slow down or reject agents; we respond by externalizing and enforcing shared language *with* agents |

[^naur]: Peter Naur, “Programming as Theory Building” (1985); reprinted in
    *Computing: A Human Activity* (1992). A local study copy may exist as
    owner-supplied markdown of the same article; the published essay is the
    citable source.
[^knuth]: Donald E. Knuth, “Literate Programming,” *The Computer Journal*
    27(2) (1984), 97–111; see also
    [the author's overview](https://cs.stanford.edu/~knuth/lp.html).
[^ronacher]: Armin Ronacher, [“The Tower Keeps Rising”](https://lucumr.pocoo.org/2026/7/13/the-tower-keeps-rising/)
    (2026-07-13).

### Surfaces and questions

The surface-by-question table is in the primer [AT-REF-3]. The positions this
repository takes on it: theory informs contracts and never replaces them;
contracts must not silently contradict theory; and process exists to keep
theory and contracts alive under agent labor—not as an end in itself.

---

## Purpose and desired feel [AT-THEORY-1]

**Agent Theory** is a practical discipline for building software with coding
agents while keeping humans in possession of the program's theory. **This
repository** is a project-neutral, repo-owned reference operating model and
starter corpus for applying that discipline.

It should feel like:

- a **shared language kit** for concepts, ownership, plans, reviews, and
  lessons—not a second product framework competing with the app,
- **progressive disclosure**: short entry for humans; machine-usable read
  order for agents; depth only where work lands,
- **honest about theory**: externalize enough to orient and refuse category
  errors; never pretend the document *is* full possession,
- **maintainable under multi-agent multi-human load**: friction is deliberate
  where identity and invariants are at stake; local work stays local.

“Simple” for this system means **a small concept count for the guidance model**,
not a small number of files. Cohesive process machinery is justified when it
protects a predictable external model (how a repo orients agents and humans).

---

## Whole-system mental model [AT-THEORY-2]

Humans and agents cooperate on a repository. Agents are strong at **local**
coherence (this function, this test, this PR) and weak at **global** product
identity unless that identity is externalized, loaded at the right scope, and
enforced when local work would redefine the product.

Agent Theory supplies:

1. **Orientation** — entry points and read orders so a zero-context agent can
   start without inventing a second constitution.
2. **Artifact roles** — theory, specs, plans, implementation docs, skills,
   lessons, coalescing state; each answers a different question.
3. **Judgment protocol** — task class, independent review, hardening for risky
   work, documentation as a completion gate.
4. **Theory transfer** — product program theory, **extended by module theory**
   where depth belongs, so “what kind of product/subsystem this is” is not
   only tribal chat.
5. **Negative knowledge** — rejected alternatives and non-goals with
   reconsider conditions, so agents do not re-litigate settled refusals.
6. **Scaffolding** — bootstrap into other repos without merging or inventing
   their product architecture.

The **hub** is the portable process and meta-theory. **Consumer repos** own
product theory, product contracts, and engineering specialization.

### Module theory: the conceptual extension rule [AT-THEORY-2.1]

**Module theory is how agents and humans grow product theory without destroying
progressive disclosure.** It is not an optional essay genre and not a second
process stack. It is the standard answer to:

> Product theory would become too long if we put this here, but agents still
> need a generative model, ownership table, and non-goals before they change
> this subsystem.

Theory is layered by **scope of work**:

```text
product program theory     →  what kind of product this is (general entry)
module / subsystem theory  →  what kind of module this is (only on entry)
contracts / fixtures       →  exact rules and inventory
code / tests               →  realization and evidence
```

| Role | Product `docs/program-theory.md` | Module theory |
|------|----------------------------------|---------------|
| **When** | Always, once the stub is replaced | When a module has its own generative rule, non-goals, or concept ownership that general entry should not carry |
| **Who loads it** | Any product-scope design or identity work | Work that **enters** that module (paths, packages, apps) |
| **Must answer** | Problem, feel, whole-program model, top concepts, product non-goals | Module ownership table, local generative model, local non-goals, local ALT/REV, required action on entry |
| **Must not** | Dump every subsystem rule | Require sibling module theories; redefine product-wide non-goals without promotion |

**Conceptual rules:** keep product theory short; put local generative depth next
to the owning code (conventional name `MODULE-THEORY.md`); load module theory
**on entry**, not on every session start; never require sibling module theories
to place work here; promote product-scope decisions upstairs rather than
stranding them forever in a module file.

Operational drafting checklist, entry-wiring procedure, and ALT/REV field
templates live in `skills/crystallize-program-theory/SKILL.md` — not here —
so session startup does not carry a second operating manual.

**When not to write module theory:** pure implementation detail, a one-off plan,
or content that belongs in a winning contract.

Humans and agents should share this sentence:

> We extend the conceptual model with **module theory** when depth is local;
> we do not inflate product theory or leave local identity only in chat.

---

## Core concepts and ownership [AT-THEORY-3]

| Concept | Meaning | Owner |
|---------|---------|--------|
| **Shared language** | Concepts, boundaries, invariants, ownership, why | Product or module theory + contracts; process enforces use |
| **Program theory (account)** | Current externalized conceptual model at product scope | Product owner (consumers); hub maintainers (this repo) |
| **Module theory (account)** | Scoped extension of product theory for one owning unit | Module owner; product theory remains apex for product-wide non-goals |
| **Process / DOM** | How work is planned, reviewed, verified, documented | This hub's operating-model spec and runbooks |
| **Winning contract** | Exact intended behavior now | Product specs / registry-style ownership in consumers |
| **Plan** | In-flight execution record | Authoring agent + human; closed via status index |
| **Lesson / coalescing** | Durable corrections; fold of sediment | Repo process; thresholds in coalescing state |
| **Skill** | Reusable task-scoped workflow | Skills lifecycle; promoted from recurrence |
| **Bootstrap** | Neutral install of process surface | This hub; consumers adapt, do not re-derive product |

A concept claimed as owner by two surfaces without an explicit propagator
role is a defect, not a discussion.

---

## Design principles [AT-THEORY-4]

1. **Humans may delegate implementation, not understanding.** Agents write
   text; humans (and theory-owning teams) remain responsible for placement
   and refusal.
2. **Surprise revises the model.** Unexpected program behavior *or*
   unexpected agent paths are evidence: “What in the theory is wrong?”
   Process failures (duplicate paths, mixed boundaries) count as theory or
   transfer failures, not only as “agents are messy.”
3. **Global vs local knowledge is the central agent failure mode.** Local
   reasonableness is cheap; redefining the product is expensive. Orientation
   and gates protect the global packet.
4. **Deliberate friction replaces lost social friction.** Agents remove the
   need to talk; shared language used to be rebuilt in review conversations.
   Plans, reviews, classes, and theory entry put friction back where identity
   is at stake (Ronacher's diagnosis).
5. **Separate questions, linked surfaces.** Spec ≠ plan ≠ implementation
   rationale ≠ theory ≠ code. Knuth's contact between explanation and
   realization is achieved by **traceability and gates**, not one master file.
6. **Negative knowledge is first-class.** Non-goals and rejected alternatives
   with “reconsider when” prevent amnesia and dogma.
7. **Scaffold is create-only and non-magical.** Bootstrap does not invent
   product architecture or merge conflicting constitutions by default.
8. **Process serves theory transfer, not reverse.** When process mass grows
   without improving orientation, refusal, or possession, cut process—not
   product identity.
9. **Extend theory by scope, not by bulk.** Product theory stays the apex;
   **module theory is the concrete way to deepen the model** for a subsystem
   without forcing every agent to load local depth at session start
   ([AT-THEORY-2.1]).

---

## What Agent Theory is not [AT-THEORY-5]

- Not a substitute for a product program theory in consumers.
- Not a claim that documents fully serialize tacit possession (Naur).
- Not big design up front: theory begins partial and is refined feature by
  feature through dialogue, specification, implementation, review, and
  evidence.
- Not a universal “more docs = better code” religion.
- Not an application framework, agent runtime, or orchestrator product.
- Not a requirement that every edit pay full class-5 ceremony (task class
  scales planning; verification floors remain).
- Not speed-and-slop optimization; throughput factories with optional code
  non-possession are a **different protocol**. Agent Theory optimizes
  **identity-preserving evolution under agent labor**.
- Not finished extraction of every practice that will ever be needed;
  dogfood revises the hub.
- Not a carrier for claims about its own efficacy. The discipline lives
  here; arguments that it works — peer observation, comparison against
  lighter workflows, case studies — belong in external writing that cites
  this repository. Falsifiers and fit statements are self-knowledge and
  stay; comparative advocacy does not. **Factual provenance and adoption
  links** (where the practices came from, which repositories use them) may
  appear in the hub README; they are not efficacy arguments.

---

## Tensions and falsifiers [AT-THEORY-6]

- **Process tower:** If ceremony grows while product residual (unwritten
  identity, unbound contracts) stays soft, the system is optimizing itself.
  *Observable:* **promotion lag** — elapsed time from a behavior shipping to
  a coded clause with a firing gate that owns it. Lag that grows while the
  process surface advances is this falsifier firing, and it is measurable
  from git dates without new tooling.
- **Unread theory:** If agents never load theory at the right scope, the
  account is theater.
- **False possession:** If humans only hold the theory of the docs, not the
  runtime, Naur possession has failed. *Probes,* in rough order of strength:
  (1) can the owner predict the class of bug an agent is about to find, before
  it reports? (2) can they design a boundary for a subsystem without reopening
  the transcript that built it? (3) does a week away leave the model intact,
  or does it have to be reread? (4) when the system misbehaves, is the feeling
  *betrayed by an invariant I know* or *surprised by a system I don't own*?
  The fourth is the cheapest and the least deniable. Possession is perishable,
  so probing recurs: at each release or each class-5 plan completion, run
  **one** probe from this list — posed to an agent or self-administered — and
  record the outcome in the plan or lessons. One probe, not a battery; the
  drill keeps the claim falsifiable rather than adding ceremony.
- **Bootstrap pollution:** If consumers run for months on the hub's
  program-theory text as if it were product identity, progressive disclosure
  failed.
- **Module sprawl without apex:** Many module theories and no product theory
  → dialect islanding. This fires on **divergence, not precedence**: local
  theory is routinely written before anyone has the words for apex theory
  (mm's `cms/ARCHITECTURE.md` predates the concept by over a year), and that
  order is healthy — practice first, name second. The failure is module
  theories that answer the *same* question differently, or that carry
  product-scope claims no apex account has ever had to reconcile.
- **Opposite optimum:** Environments that correctly choose pure speed+slop
  for short-lived or solo exploration should not be forced into full Agent
  Theory; the theory should state the fit, not annex all agentic work.
- **Register without transfer:** If predeclared, blinded paired
  probes across the currently supported model mix show no repeatable
  change in framing or correct concept use when register changes
  while propositions are held constant, narrow the account to the
  informational function. Apply the same test to citation anchors by
  removing citation and lineage cues while preserving the
  propositions attributed to them; if no material effect survives the
  predeclared threshold, retain those citations only for provenance.
- **Theory as second operating manual:** If the mandatory startup theory file
  accumulates interview scripts, full templates, and maintenance runbooks that
  belong in skills, progressive disclosure and surface roles have failed.

---

## Maintenance and extension [AT-THEORY-7]

### When to change this hub theory

Change [AT-THEORY-*] when evidence shows the **guidance system** has a wrong
problem statement, ownership model, or non-goal—not when a single consumer
needs a product rule.

### What earns a place here

A program's theory evolves through pressure and practice. If you notice that
you are doing something repeatedly, that is good evidence that you are
circling around an unwritten theory rule that should be made explicit.
Naming it is usually the whole work; the practice was already load-bearing.

The admission test for any addition proposed here, by human or agent: **can
you point at the practice it names?** A rule distilled from observed practice
is a naming. A rule reasoned from analogy, with no practice behind it, is
ceremony wearing a principle's clothes.

This test is already mechanized in places: the promotion tier mints a skill
only after a workflow recurs across three distinct citations, and the fold-up
threshold is the same test applied across repositories.

### How to extend (ladder)

1. Prefer runbooks and skills for operational detail.
2. Prefer the operating-model spec for normative process obligations.
3. Prefer lessons + coalescing for durable corrections and sediment fold.
4. Promote to this program-theory only when the **identity** of Agent Theory
   changes (new principle, new non-goal, new disclosure ladder).
5. **Consumers:** product theory → module theory when depth is local →
   contracts for exact behavior → real ALT/REV when refusals or revisions
   happen. Use `skills/crystallize-program-theory/SKILL.md` for interviews,
   templates, and entry wiring.

Negative knowledge and revisions are **first-class when real**, not a quota.
Do not pre-create empty ALT/REV slots. Field shapes and paste-ready templates
live only in the crystallize skill.

### Hybrid with speed

Inside a fixed identity envelope, high-throughput agent work is welcome.
Theory maintenance refuses to spend speed on **accidentally redefining the
product**.

---

## Crystallizing product or module theory [AT-THEORY-8]

The interview spine, one-question-at-a-time protocol, module drafting
checklist, entry-wiring procedure, and ALT/REV field templates live in
`skills/crystallize-program-theory/SKILL.md`. They are not duplicated here so
mandatory session startup does not carry a second operating manual.

Stable code **[AT-THEORY-8]** names that operational surface by reference.

---

## Revisions [AT-THEORY-9]

### [REV-AT-001] First draft externalization (2026-07-30)

Current account: Agent Theory is a discipline whose reference operating model
is this repository; identity is shared language under agent labor; progressive
theory disclosure with **module theory as the concrete extension of the product
model**; Naur/Knuth/Ronacher lineage; consumer product theory replaces hub
theory.
Supersedes: Hub README framed only as neutral scaffold without an explicit
program-theory account of the guidance system itself.
Pressure: Dogfood showed orientation speeches (“what kind of product this is”)
and module-depth theory needs that process alone does not name; peer contrast
with high-throughput slop protocols required an explicit identity statement.
Evidence:
- owner-recalled: crystallization of product and module theory practice across
  consumer dogfood (2026-07)
- contemporaneous: this first draft; later same-day clarification that module
  theory is the expected extension mechanism, not optional depth

### [REV-AT-003] The corpus carries register as well as information (2026-08-06; adopted 2026-08-07)

Current account: Guidance artifacts communicate propositions and also
establish a working register: the vocabulary, distinctions, and
intellectual lineages through which agents frame the work. The hub
therefore treats composition of always-loaded surfaces as a
capability-environment decision, not merely a style choice. Citations
can participate in that environment when they are accurately
represented and contribute concepts, distinctions, or refusals the
account actually uses. The Naur, Knuth, and Ronacher references in
this file are current examples. Register remains non-evidentiary:
fluent form can camouflage error, so correctness continues to depend
on executable gates and independent review. This corpus is, in part,
an experiment in shaping the capability environment agents draw on.
The working hypothesis is that register and citation composition
affect output framing or correct concept use. No predeclared, blinded
paired probe across the currently supported model mix has run; the
motivating observations are confounded by fluency and do not support
that hypothesis. The account stays narrow until the register
falsifier in [AT-THEORY-6] has been exercised; the falsifier is the
standing invitation to test it.
Supersedes: The prior account treated the corpus primarily as an
informational and ownership surface while leaving the role of
register and citation selection unnamed.
Pressure: The owner's deliberate use of the Naur, Knuth, and Ronacher
lineage as part of the hub's conceptual frame, together with the
simplebroker pre-release review cycle in which the same hardening
register carried both sound and unsound proposals. The owner's
motivating impression about register effects was a further pressure;
its content is recorded in the backport plan's execution log
(`docs/plans/2026-08-07-simplebroker-backport-wave-plan.md`) and is
disqualified as evidence by this revision.
Evidence:
- contemporaneous: this file's intellectual-lineage table and
  `docs/lessons.md` 2026-08-06 entries on well-formed plans and
  register symmetry (same-worktree records of the same dialogue —
  contemporaneous, not independent validation)
- owner-recalled: citation selection was intended partly to establish
  the conceptual register, confirmed 2026-08-06

### [REV-AT-002] Theory surface vs operating procedure (2026-07-30)

Current account: The mandatory startup theory account holds this repository's
*positions* on theory (not its definition), purpose, mental model, concepts,
principles, non-goals, falsifiers, the module-theory conceptual rule, and
revisions. Definition, lineage summary, surface-by-question table, and the
possession enumeration are the primer's
(`docs/specs/02-agent-theory-and-program-theory.md`), which travels to
consumers whose own theory file describes their product instead.
Interview spine, ALT/REV field
templates, module drafting checklist, and entry-wiring procedure live only in
`skills/crystallize-program-theory/SKILL.md`. Bootstrap stub stays short and
points at the skill. Stub gate: begin crystallization before *committing*
product-scope behavior — not before all design exploration.
Supersedes: Self-contained theory file that duplicated the full crystallization
methodology and templates at startup load cost.
Pressure: Independent review (2026-07-30): high context tax, three-way template
sync, and contradiction with “different surfaces answer different questions.”
Evidence:
- contemporaneous: independent review findings 4 and 5 on the program-theory
  wave; repair pass this revision records
- contemporaneous: second pass the same day — the repair moved procedure out
  but restated the definitional half in the new primer, leaving two accounts
  to synchronize; resolved by splitting definition (primer) from position
  (here) rather than by deleting either

---

## Related

- `README.md` — human entry (discipline + this reference repository)
- `docs/specs/02-agent-theory-and-program-theory.md` — definitional primer
  (what Agent Theory / program theory are; not this file's product-or-hub account)
- `docs/specs/01-development-documentation-operating-model.md` — normative process
  ([DOM-2], [DOM-3]: program theory as taxonomy and startup surface)
- `docs/agent-context/` — shared execution context and runbooks
- `skills/crystallize-program-theory/SKILL.md` — interview, templates, module
  drafting, entry wiring
- `bin/bootstrap-agent-theory` — install process scaffold + short product theory stub
