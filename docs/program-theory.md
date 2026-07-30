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
2. Use `skills/crystallize-program-theory/SKILL.md` (or the question set in
   [AT-THEORY-8]) to interview the owner until a product-specific theory can
   be written.
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

## What “program theory” means [AT-THEORY-0]

“Theory” here follows Peter Naur's *Programming as Theory Building* (1985).[^naur]
It is not a formal mathematical theory and not a synonym for requirements or
architecture diagrams. It is the **working explanatory model** that connects
affairs in the world to the shape of a program (or, here, of a guidance
system): what problem is being handled, which concepts exist, who owns them,
what is deliberately out of scope, and what evidence would show the model is
wrong.

Naur's object is “a theory of how certain affairs of the world will be handled
by, or supported by, a computer program.”[^naur] **Possession is practical, not
mnemonic.** Someone has the theory when they can:

- relate world affairs to program (or process) shape,
- justify why that shape exists,
- place a new demand without losing coherence,
- diagnose surprises that do not fit.

Memorizing this file is not possession. The fuller working theory is rebuilt
from this account together with the operating-model spec, runbooks, skills,
gates, consumer dogfood, and concrete surprises.

### Intellectual lineage

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

| Surface | Question it answers |
|---------|---------------------|
| **Program theory** (this file in the hub; product-specific in consumers) | What problem and model make the system coherent? Why these concepts and boundaries? |
| **Process / operating model** (`docs/specs/01-…`, agent-context, skills) | How do humans and agents plan, review, verify, and keep docs honest? |
| **Product contracts** (specs / winning README sections in product repos) | What exact behavior is intended now? |
| **Implementation rationale** | Why does the current realization have this shape? |
| **Code and tests / gates** | How is behavior realized, and what evidence fires? |
| **Plans and alternative records** | What change was considered, under which evidence? |

Theory informs contracts; it does not replace them. Contracts must not silently
contradict theory. Process exists to keep theory and contracts alive under
agent labor—not as an end in itself.

---

## Purpose and desired feel [AT-THEORY-1]

**Agent-theory** is a **project-neutral, repo-owned guidance system** for
software work in which coding agents are first-class collaborators.

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

Agent-theory supplies:

1. **Orientation** — entry points and read orders so a zero-context agent can
   start without inventing a second constitution.
2. **Artifact roles** — specs, plans, implementation docs, skills, lessons,
   coalescing state; each answers a different question.
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

### Module theory: the concrete extension of the model [AT-THEORY-2.1]

**Module theory is how agents and humans are expected to grow product theory
without destroying progressive disclosure.** It is not an optional essay genre
and not a second process stack. It is the standard answer to:

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

**Concrete extension steps (consumers):**

1. Keep product theory short and load-bearing for **product** identity.
2. When a change set repeatedly needs orientation that is **not** product-wide,
   write module theory **next to the owning code** (conventional name:
   `MODULE-THEORY.md` in the module root, or a single agreed path documented
   from product theory / AGENTS).
3. Give the file the same metadata shape as product theory: Status, Owner,
   Boundary, Verification, Required action (“read on entry to … before
   changing …”).
4. Include an **ownership table** (owner / consumer / propagator). Two modules
   claiming owner of the same concept is a gate failure.
5. State **what the module is not** and record rejected alternatives with
   reconsider conditions.
6. Point exact rules at contracts/fixtures; do not duplicate them as theory.
7. If a decision is really product-scope, **promote** it to product theory
   (or mark it parked-for-promotion); do not let module theory become a shadow
   product constitution.
8. Wire entry: agents working in that tree read module theory **after** product
   theory (or product overview) and **before** changing the module’s classes,
   rules, or public shape. Do not add every module theory to global session
   `read_order`.

**Module theory must be actionable without reading sibling modules.** Needing
another module’s theory to place work in this one is a defect in the ownership
table—report it, do not route around it.

**When not to write module theory:** pure implementation detail, a one-off plan,
or content that belongs in a winning contract. Prefer a plan or spec delta until
a generative model or non-goal set stabilizes.

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

## What agent-theory is not [AT-THEORY-5]

- Not a substitute for a product program theory in consumers.
- Not a claim that documents fully serialize tacit possession (Naur).
- Not a universal “more docs = better code” religion.
- Not an application framework, agent runtime, or orchestrator product.
- Not a requirement that every edit pay full class-5 ceremony (task class
  scales planning; verification floors remain).
- Not speed-and-slop optimization; throughput factories with optional code
  non-possession are a **different protocol**. Agent-theory optimizes
  **identity-preserving evolution under agent labor**.
- Not finished extraction of every practice that will ever be needed;
  dogfood revises the hub.
- Not a carrier for claims about its own efficacy. The discipline lives
  here; arguments that it works — peer observation, comparison against
  lighter workflows, case studies — belong in external writing that cites
  this repository. Falsifiers and fit statements are self-knowledge and
  stay; comparative advocacy does not. A repository that argues for itself
  invites evaluation of the argument instead of use of the method, and the
  two age on different clocks.

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
  The fourth is the cheapest and the least deniable.
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
  for short-lived or solo exploration should not be forced into full agent-
  theory; the theory should state the fit, not annex all agentic work.

---

## Maintenance and extension [AT-THEORY-7]

### When to change this hub theory

Change [AT-THEORY-*] when evidence shows the **guidance system** has a wrong
problem statement, ownership model, or non-goal—not when a single consumer
needs a product rule.

### What earns a place here

A program's theory evolves through pressure and practice. If you notice that
you are doing something repeatedly, that is good evidence that you are
circling around an unwritten theory rule that should be made explicit —
asking the same question before every design discussion, writing the same
kind of document next to different modules, correcting the same class of
mistake. Naming it is usually the whole work; the practice was already
load-bearing.

The converse is the admission test for any addition proposed here, by human
or agent: **can you point at the practice it names?** A rule distilled from
observed practice is a naming. A rule reasoned from analogy, with no practice
behind it, is ceremony wearing a principle's clothes — it reads well and
fails the first time someone asks what they would do differently with it.

This test is already mechanized in places: the promotion tier mints a skill
only after a workflow recurs across three distinct citations, and the fold-up
threshold is the same test applied across repositories. "Performative
overengineering" in the review lens is what this test rejects.

Worked examples: asking "is this *simplebroker*ness?" before a design
discussion became program theory; `cms/ARCHITECTURE.md` (2025) and its
siblings became module theory; hand-pruning the lessons ledger became
coalescing. A proposed tool that would scan the ecosystem and report which
falsifiers were firing went the other way — invented from analogy, with no
practice behind it — and did not survive its first "what would you do
differently?"

### How to extend the process surface

1. Prefer runbooks and skills for operational detail.
2. Prefer the operating-model spec for normative process obligations.
3. Prefer lessons + coalescing for durable corrections and sediment fold.
4. Promote to this program-theory only when the **identity** of agent-theory
   changes (new principle, new non-goal, new disclosure ladder).

### How consumers extend theory

Treat extension as a **ladder**, not a pile of docs:

1. **Product theory** — write `docs/program-theory.md` (replace stub). This is
   the apex shared language for the product.
2. **Module theory** — when product theory would become too verbose **or**
   agents repeatedly need local generative rules/non-goals, **extend the model
   with module theory** per [AT-THEORY-2.1] (conventional `MODULE-THEORY.md` at
   the module root). This is the normal, expected extension—not an exception.
3. **Contracts** — keep specs, fixtures, and codes as exact behavior; theory
   stays judgment-shaped unless carefully dual-homed.
4. **Decision cases** — record ALT/REV when agents re-propose rejected shapes
   or a sweep revises a generative rule; park product-scope ALTs for promotion
   rather than stranding them only in a module file forever.
5. **Crystallize** — use `skills/crystallize-program-theory/SKILL.md` for either
   product or module interviews; say which scope you are extending.

### Hybrid with speed

Inside a fixed identity envelope, high-throughput agent work is welcome.
Theory maintenance refuses to spend speed on **accidentally redefining the
product**. That is the value proposition relative to pure slop protocols.

### How to record decisions [AT-THEORY-7.1]

Negative knowledge and revisions are **first-class when real**, not a quota.

**Do:** write an ALT when something competent is refused or deferred; write a
REV when the current account of the theory changes.  
**Do not:** pre-create empty `[ALT-001]` files, empty decision directories, or
zero-length placeholders. Absence means none yet.

Paste-ready shapes (same as the product bootstrap stub appendix):

#### Rejected or deferred alternative

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

#### Theory revision

```markdown
### [REV-<SCOPE>-<NNN>] Short title

Current account: <revised theory — put current first>
Supersedes: <short prior account; do not let it compete with current>
Pressure: <what made the prior account inadequate>
Evidence:
- contemporaneous | owner-recalled | inferred | unknown: <source>
```

Use these under a “Revisions and decision cases” section of product or module
theory. Module files may hold local ALTs; product-wide non-goals should be
promoted to product theory when stable.

---

## Crystallizing a product program theory [AT-THEORY-8]

Prefer the skill `skills/crystallize-program-theory/SKILL.md` for an
interview session. The questions below are the same spine for humans writing
without the skill.

Work **one question at a time** when interviewing. Look up facts from the
repo; put **decisions** to the owner.

### Spine questions

1. **Problem world** — What affairs of the world does this program handle?
   For whom? What fails if it does not exist?
2. **Desired feel** — What should using it feel like in one paragraph?
3. **Whole-program metaphor** — In three to seven bullets, what is the
   mental model (not the file tree)?
4. **Core concepts** — Name each concept, its meaning, and its **owner**
   (this product / a module / the user / another system).
5. **Matching surface** — How do CLI, API, UI, or docs express the same
   model without inventing a second product?
6. **Non-goals** — What will competent people propose that you will refuse?
   Why? When would you reconsider?
7. **Generative rule** — Is there one question that organizes a large part
   of the design (as control locality might organize a taxonomy)?
8. **Delivery / safety honesty** — Where can work be lost, duplicated, or
   weakly authenticated? Name the guarantee narrowly.
9. **Tensions** — What live tensions would falsify the account if they
   worsened?
10. **Extension by module theory** — What depth should become module theory
    (ownership table, local generative rule, local non-goals) so product theory
    stays short? Which path owns that file?
11. **Possession test** — What surprises (bugs or bad agent paths) would
    force a theory revision rather than a local patch?
12. **Replacement check** — If this were only a README restatement, what
    judgment would still be missing?

Stop when the owner can **place a feature**, **refuse a category error**,
and **predict a failure mode** without re-deriving the product from scratch.

---

## Revisions [AT-THEORY-9]

### [REV-AT-001] First draft externalization (2026-07-30)

Current account: Agent-theory is a guidance system whose identity is shared
language under agent labor; progressive theory disclosure with **module theory
as the concrete extension of the product model**; Naur/Knuth/Ronacher lineage;
consumer product theory replaces hub theory.
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

---

## Related

- `README.md` — human entry (this hub)
- `docs/specs/01-development-documentation-operating-model.md` — normative process
- `docs/agent-context/` — shared execution context and runbooks
- `skills/crystallize-program-theory/SKILL.md` — interview to write product or module theory
- `bin/bootstrap-agent-theory` — install process scaffold + product theory stub
  (module theory and ALT/REV are conventions + templates, not empty files)
