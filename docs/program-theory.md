# Agent-Theory Program Theory

Status: Active — first draft
Owner: agent-theory maintainers
Boundary: Conceptual identity and design judgment for **this guidance system**,
not the product behavior of any repository that installs it.
Verification: Owner and independent semantic review; structural consistency
with `docs/specs/01-development-documentation-operating-model.md` and the
bootstrap surface.
Required action: Read this file before changing the purpose of the hub, the
document roles, the scope-loading rules, or the bootstrap defaults. Either
conform to this theory or propose an explicit revision.

---

## Product repositories must replace this file

In a product or library repository, `docs/program-theory.md` describes **that
product**. In this hub repository, `docs/program-theory.md` describes the
**Agent Theory guidance system itself**.

When a product or library repository installs this starter kit:

1. **Replace `docs/program-theory.md` with the product's own theory.** Write an
   account of what problem that product solves, its core concepts, who owns
   each boundary, what it refuses to build, and what evidence would show the
   model is wrong.
2. **Interview the owner to draft the theory.** Run
   `skills/crystallize-program-theory/SKILL.md` to ask the owner one decision
   question at a time.
3. **Keep the top-level product theory short.** When a specific subsystem or
   package needs its own design rule, ownership table, or local non-goals,
   write a **module theory** file (`MODULE-THEORY.md`) next to that code
   (`[AT-THEORY-2.1]`) rather than expanding `docs/program-theory.md`.
4. **Do not treat a stub or hub theory as product authority.** Until the file
   is replaced, treat any starter text as process orientation only.

To prevent mix-ups, `bin/bootstrap-agent-theory` installs a short `Status: Stub`
placeholder in new product repositories rather than copying this hub file.
Module theory files are not pre-created as blank stubs; create a
`MODULE-THEORY.md` file only when a subsystem genuinely needs local depth.

---

## Core claims about program theory [AT-THEORY-0]

A **program theory** is a team's working mental model of how a software system
solves its problem and why it is structured the way it is. (If the term is new,
read the definitional primer in
`docs/specs/02-agent-theory-and-program-theory.md` `[AT-REF-2]` first.) While
the primer defines the terms, this section states the contestable positions
that shape this repository.

Our use of "theory" follows Peter Naur's *Programming as Theory Building*
(1985).[^naur] **Holding a theory is a practical skill, not memorization.** A
person who holds the theory can map real-world demands onto the code's
structure, explain why each boundary exists, reject features that do not fit,
and diagnose unexpected bugs. No single file can hold all of that on its own;
humans and agents rebuild the working model by combining this written account
with specs, runbooks, skills, executable gates, and runtime surprises.

### What we take—and refuse—from our sources

Three sources shape Agent Theory. In the table below, the right-hand column is
just as important as the middle column: what we **refuse** to adopt from each
author is where our design makes its sharpest bets.

| Source | What we adopt | What we refuse to adopt |
|--------|---------------|-------------------------|
| **Peter Naur (1985)** | Programming is theory building; documentation is secondary to holding the working mental model; the quality of future modifications depends on holding that theory; **"program death"** occurs when the people who hold the theory leave.[^naur] | The fatalistic view that a theory can never be written down usefully. We write a concise *current account* (`docs/program-theory.md`) to transfer framing to agents and teammates, without pretending the file replaces human understanding. |
| **Donald Knuth (1984)** | Explanations exist to build human understanding and must stay tied to the running code.[^knuth] | Putting all prose and code into one monolithic literate source file. Instead, we separate theory, specs, plans, implementation notes, and code into distinct files linked by traceability checks. |
| **Armin Ronacher (2026), "The Tower Keeps Rising"** | Shared language—concepts, boundaries, invariants, ownership, and *why*—is the scarce resource in AI-assisted coding. Coding agents remove the friction that used to force teams to maintain that language, allowing a codebase to keep growing after shared understanding has collapsed.[^ronacher] | The conclusion that the only answer is to reject agents or slow down to manual coding. Instead, we write down the shared language and enforce it *with* agents and automated gates. |

[^naur]: Peter Naur, "Programming as Theory Building" (1985); reprinted in
    *Computing: A Human Activity* (1992). A local study copy may exist as
    owner-supplied markdown of the same article; the published essay is the
    citable source.
[^knuth]: Donald E. Knuth, "Literate Programming," *The Computer Journal*
    27(2) (1984), 97–111; see also
    [the author's overview](https://cs.stanford.edu/~knuth/lp.html).
[^ronacher]: Armin Ronacher, ["The Tower Keeps Rising"](https://lucumr.pocoo.org/2026/7/13/the-tower-keeps-rising/)
    (2026-07-13).

### How theory relates to specs and process

The primer (`[AT-REF-3]`) lists which document answers which question. Three
rules govern how those documents interact here:

1. **Theory frames specs, but never overrides them.** Use program theory to
   decide whether an idea fits the system and where it belongs; use specs to
   define exact behavior.
2. **Specs must not silently contradict the theory.** When a spec change
   conflicts with `docs/program-theory.md`, pause and update one of them
   explicitly.
3. **Process exists to keep theory and specs honest under agent speed.** Any
   process rule that does not improve orientation, error detection, or human
   understanding should be cut.

---

## Purpose and desired feel [AT-THEORY-1]

**Agent Theory** is a practical discipline for building software with coding
agents while keeping humans in possession of the program's theory. **This
repository** is the project-neutral reference operating model and starter kit
for applying that discipline.

Working in an Agent Theory repository should feel like:

- **Using a shared vocabulary** for concepts, ownership, plans, reviews, and
  lessons—not learning a heavyweight framework that competes with your product.
- **Loading only what the task needs**: a short overview at session start, and
  deeper module or runbook rules only when your task enters that area.
- **Staying honest about what docs can do**: writing down enough of the mental
  model to orient agents and block category errors, without pretending a
  markdown file replaces a human who understands the code.
- **Putting friction only where it counts**: small, local fixes move fast, while
  changes that touch boundaries, public contracts, or product identity hit
  deliberate review and verification checkpoints.

Here, "simple" means **few moving concepts**, not a tiny number of files.
Separate files for theory, specs, plans, and lessons are worth having because
each file has one clear job.

---

## Whole-system mental model [AT-THEORY-2]

Coding agents are strong at **local** work—writing a function, fixing a test,
or drafting a pull request—and weak at **global** product judgment unless the
system's identity is written down, loaded at the right time, and checked when a
local change would alter the product's shape.

To close that gap between local agent competence and global system coherence,
Agent Theory provides six pieces:

1. **Session orientation** — Clear entry points (`AGENTS.md`, `README.md`) and
   a fixed read order so a zero-context agent starts with the repository's own
   rules instead of guessing.
2. **Separate document roles** — Dedicated files for program theory, behavioral
   specs, execution plans, implementation rationale, reusable skills, lessons
   learned, and coalescing state, so each file answers one question.
3. **Scaled judgment checkpoints** — Task classification (`[DOM-15]`),
   cross-family independent review (`[DOM-11]`), risk hardening, and
   documentation updates before work is called done.
4. **Layered theory documents** — A short top-level product theory
   (`docs/program-theory.md`) extended by local **module theories**
   (`MODULE-THEORY.md`) where a subsystem needs deeper rules.
5. **Recorded negative knowledge** — Explicit non-goals and rejected
   alternatives (`[ALT-*]`) with `"reconsider when"` conditions, so agents do
   not keep re-proposing designs the owner already rejected.
6. **A safe starter installer** — `bin/bootstrap-agent-theory`, which copies
   the process files and gates into a repository without overwriting existing
   files or inventing product architecture.

This **hub repository** maintains the portable process, gates, and guidance.
Each **product repository** owns its product theory, behavioral specs, and
codebase-specific engineering rules.

### Module theory: extending the model without bloating startup [AT-THEORY-2.1]

As a codebase grows, putting every subsystem's rules into
`docs/program-theory.md` would make the startup file too long to read cleanly.
At the same time, leaving a complex subsystem's design rules unwritten forces
every agent to guess. **Module theory** solves that tension:

> Keep the top-level product theory short, and put subsystem-specific concepts,
> ownership tables, and non-goals in a `MODULE-THEORY.md` file right next to
> that module's code.

Documents load in layers based on the **scope of the task**:

```text
product program theory     →  what kind of product this is (loaded at session start)
module / subsystem theory  →  what kind of module this is (loaded only on entry to that module)
specs / fixtures           →  exact behavioral rules and test tables
code / tests               →  running implementation and automated proof
```

| Question | Top-level `docs/program-theory.md` | Local `MODULE-THEORY.md` |
|----------|------------------------------------|--------------------------|
| **When is it written?** | For every product repository (replacing the bootstrap stub) | Only when a subsystem has its own design rule, concept ownership, or non-goals that should not clutter session startup |
| **Who reads it?** | Every session doing product-scope design, review, or implementation | Only agents and humans whose task **enters** that module's directory |
| **What must it contain?** | Problem statement, desired feel, whole-program model, core concepts, product-wide non-goals, and falsifiers | Module ownership table, local design model, local non-goals, local `[ALT-*]`/`[REV-*]` records, and required action on entry |
| **What must it avoid?** | Dumping every package's internal rules into the root file | Requiring readers to load sibling module theories, or overriding product-wide non-goals without updating the root theory |

Five rules keep module theories clean:

1. Keep `docs/program-theory.md` short enough to read at session start.
2. Place local theory next to the code it governs (typically `<module>/MODULE-THEORY.md`).
3. Load a module theory **on entry to that module**, not at every session start.
4. Keep each module theory self-contained beneath `docs/program-theory.md`—an
   agent should never have to read three sibling module theories just to understand
   one module.
5. When a local decision turns out to affect the whole product, promote it into
   `docs/program-theory.md`.

Do **not** write a module theory for routine implementation details, one-off
execution plans, or exact behavioral rules that belong in a spec. The step-by-step
interview, drafting checklist, and `[ALT-*]`/`[REV-*]` templates live in
`skills/crystallize-program-theory/SKILL.md` so session startup stays lean.

---

## Core concepts and ownership [AT-THEORY-3]

Every core concept in the workflow has one owning surface:

| Concept | What it means | Owning surface |
|---------|---------------|----------------|
| **Shared language** | The concepts, boundaries, invariants, ownership rules, and *why* behind the system | Product or module theory + specs; enforced by the review and gate process |
| **Program theory** | The written mental model of the whole product (or, in this repo, the hub) | `docs/program-theory.md` (owned by the product owner, or hub maintainers here) |
| **Module theory** | A local extension of the product theory for one subsystem | `<module>/MODULE-THEORY.md` (owned by the module owner under the product theory) |
| **Process (`[DOM-*]`)** | How tasks are classified, planned, reviewed, verified, and documented | `docs/specs/01-development-documentation-operating-model.md` and `docs/agent-context/` |
| **Winning contract** | The exact behavior the software must exhibit right now | Product specs in `docs/specs/` (and authoritative README sections where declared) |
| **Plan** | The step-by-step execution record for a non-trivial change | `docs/plans/` + `docs/plans/README.md` status index |
| **Lessons and coalescing** | Reusable corrections from past mistakes, plus periodic distillation of old records | `docs/lessons.md` and `docs/coalescing.md` (`[DOM-14]`) |
| **Skill** | A reusable step-by-step workflow promoted after recurring use | `skills/<name>/SKILL.md` |
| **Bootstrap** | Installing the starter files and gates into a product repository | `bin/bootstrap-agent-theory` |

If two documents claim to own the same rule without one clearly pointing to the
other as canonical, treat that overlap as a documentation bug and fix it.

---

## Design principles [AT-THEORY-4]

1. **Humans may delegate implementation, not understanding.** Agents can draft
   code, tests, and docs, but the human owner remains responsible for deciding
   what belongs in the system and what to refuse.
2. **Treat every surprise as evidence that the mental model has a gap.** When
   the code behaves unexpectedly *or* an agent takes a strange path, ask:
   *"What in our written theory or specs made that look reasonable?"* Duplicate
   code paths and blurred boundaries are failures of shared understanding, not
   just "agents being messy."
3. **Bridge the gap between local agent competence and global product identity.**
   An agent can easily write a locally clean patch that quietly breaks a
   system-wide invariant or non-goal. Session-start orientation and automated
   gates protect the whole-system design.
4. **Deliberate friction replaces lost social friction.** Because coding agents
   do not need hallway conversations to write code, teams lose the everyday
   discussions that used to keep concepts aligned (Ronacher's diagnosis). Task
   classes, plans, cross-family reviews, and theory checks put deliberate
   pauses back where product identity is at stake. The friction is the point:
   every guardrail — task classification, independent cross-family review,
   refused-alternative records, and governed suppression registries — exists
   to make locally plausible regressions hard to rationalize without first
   confronting the empirical evidence that produced the current shape.
5. **One question per document, linked by automated checks.** A spec is not a
   plan, a plan is not an implementation note, and an implementation note is
   not a program theory. We achieve Knuth's goal—keeping explanation tied to
   working code—through bidirectional links and gate scripts rather than a
   single giant file.
6. **Record what you refuse, not just what you build.** Writing down non-goals
   and rejected alternatives (`[ALT-*]`) along with the exact conditions that
   would make you reconsider them stops agents from re-proposing rejected ideas
   and stops old decisions from turning into unquestioned dogma.
7. **The bootstrap installer is safe and non-magical.** `bin/bootstrap-agent-theory`
   copies starter files without overwriting existing work or inventing product
   architecture.
8. **Process serves understanding, never the reverse.** When a process rule adds
   ceremony without helping humans and agents orient, reject bad ideas, or prove
   correctness, delete or simplify the process rule.
9. **Extend theory by scope, not by making the root file longer.** Keep
   `docs/program-theory.md` short and add `<module>/MODULE-THEORY.md` files for
   subsystem depth (`[AT-THEORY-2.1]`).
10. **Encode program "feel" and composable operations up front ("taste up
    front", not BDUF; `[REV-AT-005]`).** Coding agents cannot infer aesthetic
    taste or ergonomic feel from abstract box-and-arrow boundaries alone. A
    product's program theory should communicate its **feel**—its command/API
    grammar (e.g., top-level reflex verbs vs. `noun verb`), its core composable
    operations (*"here are our operations, build on these"*), and concrete taste
    anchors—while leaving internal storage schemas and implementation machinery
    to be proved through vertical end-to-end slices.

---

## What Agent Theory is not [AT-THEORY-5]

- **Not a replacement for your product's own theory.** Installing this hub's
  files gives you a process scaffold; you still have to write your product's
  `docs/program-theory.md`.
- **Not a claim that markdown files can replace a human's mental model** (Naur).
- **Not big design up front.** Fixing a program's **feel, command grammar,
  composable operations, and trust boundaries** up front is *taste up front*,
  not BDUF (`[REV-AT-005]`). What Agent Theory refuses is locking in premature
  internal schemas or building horizontal framework layers in isolation before
  testing a vertical slice against reality. A program theory starts partial and
  is revised as features are specified, built, reviewed, and tested.
- **Not a "more documentation is always better" philosophy.** Unread or
  duplicate documentation is a liability; coalescing exists to shrink it.
- **Not an application framework, agent runtime, or multi-agent orchestrator.**
- **Not heavyweight ceremony for every tiny edit.** Task classification
  (`[DOM-15]`) keeps small fixes lightweight while preserving test and gate
  standards.
- **Not a high-volume "software factory" where humans never read or understand
  the code.** Unsupervised throughput workflows optimize for a different goal;
  Agent Theory is for codebases where humans intend to keep understanding and
  steering the system as agents help build it.
- **Not a frozen rulebook.** Real friction in product repositories drives
  updates to this hub.
- **Not a marketing brochure.** This repository defines the workflow, its
  non-goals, and how to test whether it is failing. Arguments comparing its
  effectiveness against other workflows belong in external articles or case
  studies, though the root `README.md` may link to the repositories where these
  practices originated and run today.

---

## How to tell if this model is failing (tensions and falsifiers) [AT-THEORY-6]

A real theory names the evidence that would show it is failing:

- **The process tower (ceremony outgrowing the product):** If process rules keep
  expanding while product specs and theory lag behind shipped code, the
  workflow is serving itself instead of the software.
  - *How to measure it:* Check **promotion lag** in Git history—the time between
    shipping a behavior change and landing the spec clause and automated test
    that govern it. If promotion lag grows while process docs expand, this
    failure mode is firing.
- **Unread theory:** If agents make design decisions or reviews without reading
  `docs/program-theory.md` (or the relevant `MODULE-THEORY.md`), the file is
  shelfware.
- **False possession (knowing the docs, not the system):** If the human owner
  can recite the markdown files but cannot reason about the running code, Naur
  possession has failed.
  - *Four self-test questions (from hardest to easiest):*
    1. Can you predict the kind of bug an agent is about to uncover before it
       finishes investigating?
    2. Can you sketch a clean boundary for a new subsystem feature without
       re-reading the chat transcript that built the subsystem?
    3. After a week away from the repo, is your mental model still intact
       without re-reading the docs?
    4. When the program breaks, do you feel *betrayed by an invariant you know*
       or *surprised by a system you do not really own*?
  - *Habit:* Because human understanding fades over time, run **one** of these
    four checks at each release or Class-5 completion and note the result in the
    plan or `docs/lessons.md`.
- **Unreplaced bootstrap stubs:** If a product repository runs for months with
  a `Status: Stub` file (or with the hub's guidance theory still sitting in
  `docs/program-theory.md`), the onboarding flow has failed.
- **Module theories without a shared product theory:** It is normal and healthy
  for a team to write local architecture notes before writing a top-level
  `docs/program-theory.md` (for example, `mm`'s `cms/ARCHITECTURE.md` predated
  its product theory by over a year). The failure mode fires when multiple
  module theories **contradict each other** or make product-wide claims that no
  top-level `docs/program-theory.md` reconciles.
- **Forcing heavy ceremony onto throwaway prototypes:** Short-lived scripts and
  solo throwaway experiments do not need full Agent Theory ceremony; the model
  should state clearly where it fits instead of claiming every project needs it.
- **Register without transfer (vocabulary that does not improve framing):**
  This corpus uses vocabulary and citations from Naur, Knuth, and Ronacher on
  the hypothesis that they help agents frame problems and apply concepts
  accurately. To test that hypothesis, run **predeclared, blinded paired
  probes** across the currently supported model mix that hold the underlying
  rules (propositions) constant while varying the vocabulary (register):
  - *Register test:* If changing the register produces no repeatable improvement
    in problem framing or accurate concept use above the predeclared threshold,
    strip the extra vocabulary and keep only the plain informational rules.
  - *Citation test:* Run the same paired test by removing the named citations
    and lineage cues while keeping the rules attributed to them; if no material
    effect survives the predeclared threshold, keep those citations only for
    historical provenance.
- **Turning `docs/program-theory.md` into a second operating manual:** If this
  startup file fills up with interview scripts, copy-paste templates, and
  step-by-step runbooks that belong in `skills/` or `docs/agent-context/`,
  session startup will bloat and document boundaries have failed.

---

## Maintaining and extending this hub [AT-THEORY-7]

### When to edit this file

Update `[AT-THEORY-*]` only when evidence shows that the **guidance system
itself** has a flawed problem statement, document-ownership rule, or non-goal—not
when a single product repository needs a local engineering rule.

### The two-screen test for folding rules into the hub

When a human or agent proposes lifting a lesson, principle, or runbook rule from
a product repository into `agent-theory`, the candidate must pass **both**
screens below:

1. **Screen 1 — Real practice, not analogy:** Can you point to the concrete
   commits and incidents where this rule did real work? A rule distilled from
   repeated practice earns its place; a rule invented from pure analogy is
   ceremony dressed up as a principle. (This is why skill promotion requires
   3 distinct citations and cross-repo fold-up normally requires 2+ independent
   repository lineages.)
2. **Screen 2 — Discipline-level, not product-specific (`[REV-AT-004]`):** Is
   the rule about **how humans and agents build, transfer understanding, plan,
   review, verify, coalesce, or refuse** across any codebase? If a rule is a
   domain or runtime design choice (for example, how a queue checks live process
   state before deleting a file, or which Git flag a release script uses), it
   belongs in that product's own theory or specs—even if two products happen to
   use the same engineering pattern. Only the discipline-level planning or
   review lesson ascends to the hub.

### Where to put new guidance (the extension ladder)

Put new guidance in the narrowest document that owns that kind of rule:

1. **Operational checklists and how-tos** → `docs/agent-context/runbooks/` or
   `skills/`.
2. **Normative process requirements** →
   `docs/specs/01-development-documentation-operating-model.md` (`[DOM-*]`).
3. **Specific mistakes to avoid and periodic cleanup** → `docs/lessons.md` and
   `docs/coalescing.md`.
4. **Core identity, principles, or non-goals of Agent Theory** → this file
   (`docs/program-theory.md`).
5. **In product repositories** → top-level `docs/program-theory.md` for product
   identity → `<module>/MODULE-THEORY.md` for subsystem depth → `docs/specs/`
   for exact behavior → `[ALT-*]` / `[REV-*]` records when real refusals or
   revisions occur.

Record `[ALT-*]` (rejected alternatives) and `[REV-*]` (theory revisions) only
when a real decision or revision happens—never create empty placeholder sections
to fill a template.

### Moving fast inside clear boundaries

Once a product's boundaries, non-goals, and specs are clear, fast multi-agent
implementation inside those boundaries is a strength. Agent Theory only refuses
to trade away understanding of **what the product is** in exchange for raw
typing speed.

---

## Crystallizing product or module theory [AT-THEORY-8]

The step-by-step owner interview, module-theory drafting checklist, read-order
wiring instructions, and `[ALT-*]`/`[REV-*]` templates live in
`skills/crystallize-program-theory/SKILL.md`. Keeping that procedure in a skill
rather than in `docs/program-theory.md` keeps session startup fast. Stable code
**[AT-THEORY-8]** cites that skill as the canonical owner of the crystallization
workflow.

---

## Revision history [AT-THEORY-9]

### [REV-AT-001] First written program theory for the hub (2026-07-30)

- **Current account:** Agent Theory is an engineering discipline whose reference
  operating model is this repository. It keeps humans in possession of a
  program's theory using shared vocabulary, short top-level product theories
  extended by local **module theories** (`[AT-THEORY-2.1]`), Naur/Knuth/Ronacher
  foundations, and a bootstrap stub that product repositories replace with their
  own theory.
- **Supersedes:** Framing the repository only as a neutral doc-template scaffold
  with no explicit program theory of its own.
- **Why it changed (pressure):** Day-to-day use across product repositories
  showed that teams repeatedly needed a place to state *"what kind of product
  this is"* and *"what this subsystem owns"*—questions that process rules alone
  do not answer. Contrasting this workflow with high-volume "software factory"
  approaches also required stating our core goal explicitly.
- **Evidence:**
  - *Owner-recalled:* Crystallizing product and module theories across consumer
    repositories in July 2026.
  - *Contemporaneous:* Initial draft of `docs/program-theory.md` and same-day
    refinement establishing `MODULE-THEORY.md` as the standard way to add
    subsystem depth.

### [REV-AT-002] Separating theory claims from interview procedures (2026-07-30)

- **Current account:** `docs/program-theory.md` holds this repository's core
  claims, mental model, ownership table, principles, non-goals, falsifiers, and
  revision log. General definitions of "Agent Theory" and "program theory" live
  in the primer (`docs/specs/02-agent-theory-and-program-theory.md`), which is
  copied into product repositories. The interview script, `[ALT-*]`/`[REV-*]`
  templates, and module-theory checklist live only in
  `skills/crystallize-program-theory/SKILL.md`. Product repositories may explore
  while `docs/program-theory.md` is a `Stub`, and replace the stub before
  committing product behavior or architecture.
- **Supersedes:** Packing the full interview script, templates, and general
  definitions directly into `docs/program-theory.md`.
- **Why it changed (pressure):** Independent review on 2026-07-30 pointed out
  that keeping interview scripts and templates in the startup theory file wasted
  context tokens on every session, created three duplicate copies of the
  templates to keep in sync, and violated our own rule that each file answers
  one question.
- **Evidence:**
  - *Contemporaneous:* Independent review findings 4 and 5 on the 2026-07-30
    program-theory wave, plus the follow-up pass splitting definitions (into the
    primer) from hub-specific positions (in this file).

### [REV-AT-003] Why the corpus names its intellectual sources—and how to test if that helps (2026-08-06; adopted 2026-08-07)

- **Current account:** Guidance files do two things at once: they state rules
  (propositions), and they establish a working **register**—the vocabulary,
  distinctions, and intellectual lineages through which agents frame the work.
  Choosing what goes into always-loaded startup files is therefore a decision
  about the agent's working environment, not merely a style choice. Citations
  earn their place when they are accurately represented and supply concepts,
  distinctions, or refusals the account actually uses (such as the Naur, Knuth,
  and Ronacher references in this file).
  - *Register is never evidence of correctness:* Fluent phrasing can disguise
    bad reasoning, so correctness continues to depend on executable gates and
    independent review.
  - *Untested hypothesis and falsifier:* Our working hypothesis is that
    register and citation choices affect output framing or accurate concept
    use. **No predeclared, blinded paired probe across the currently supported
    model mix has run yet**; our informal observations are confounded by
    fluency and do not prove that hypothesis. Until the `Register without
    transfer` falsifier in `[AT-THEORY-6]` is run, this claim stays narrow.
- **Supersedes:** Treating guidance files purely as informational rule lists
  while leaving the role of vocabulary and citation selection unnamed.
- **Why it changed (pressure):** The owner deliberately selected the Naur,
  Knuth, and Ronacher lineage to frame the hub, while SimpleBroker's
  pre-release review cycle showed that the exact same "hardening" register
  carried both sound and unsound proposals. The owner's initial impression
  about register effects (recorded in
  `docs/plans/2026-08-07-simplebroker-backport-wave-plan.md`) was an additional
  prompt for this revision, and is explicitly **disqualified as evidence** by
  this revision.
- **Evidence:**
  - *Contemporaneous:* The lineage table in `[AT-THEORY-0]` and the 2026-08-06
    entries in `docs/lessons.md` on well-formed plans and register symmetry
    (same-worktree records of the same dialogue, not independent validation).
  - *Owner-recalled:* Citation selection was intended partly to establish the
    conceptual register (confirmed 2026-08-06).

### [REV-AT-004] Folding rules into the hub requires both real practice and discipline-level scope (2026-08-07)

- **Current account:** Lifting a rule from a product repository into
  `agent-theory` requires passing two screens (`[AT-THEORY-7]`): Screen 1 checks
  that the rule comes from real, cited practice; Screen 2 checks that the rule
  is about the **engineering discipline itself** (how humans and agents plan,
  review, verify, transfer understanding, or coalesce) rather than a
  product-specific runtime or tool design. Even if two product repositories use
  the same runtime precondition, that engineering rule belongs in their product
  theories; only the planning or review lesson ascends to the hub.
- **Supersedes:** Using the practice test (Screen 1) alone, which allowed
  genuinely recurring product-engineering rules to be proposed as hub rules.
- **Why it changed (pressure):** In a 2026-08-07 session, an agent proposed
  folding a product-engineering rule (preconditions on destructive runtime
  operations) into the hub because it had appeared independently in two product
  repositories. The owner rejected moving product architecture into the hub and
  stated the two-screen boundary.
- **Evidence:**
  - *Contemporaneous:* The 2026-08-07 review dialogue and `taut`'s
    `[REV-THEORY-001]`, which kept the runtime rule in `taut`'s product theory
    while recording the cross-repository review lesson for the hub.

### [REV-AT-005] Program feel, command grammar, and composable operations belong in program theory ("taste up front", not BDUF) (2026-10-15)

- **Current account:** A product's program theory (`docs/program-theory.md`)
  must communicate not only problem boundaries and concept ownership, but also
  the program's **intrinsic feel and compositional idiom**: how its surface
  speaks (e.g., top-level reflex verbs vs. `noun verb` grammar), which core
  operations new work must compose from rather than inventing side doors, and
  concrete "taste anchors" (illustrative commands or API idioms). Encoding
  taste, idiom, and composable operations up front is **not** Big Design Up
  Front (BDUF)—coding agents cannot infer aesthetic or ergonomic taste from
  abstract box-and-arrow diagrams alone. What Agent Theory avoids as BDUF is
  locking in premature internal storage schemas or building horizontal framework
  layers in isolation before proving a vertical end-to-end slice against
  reality (`[AT-THEORY-4]` §10, `[AT-THEORY-5]`, `[AT-REF-2]`, `[AT-REF-4]`).
- **Supersedes:** Leaving the role of concrete command grammar and composable
  operational feel implicit in `docs/program-theory.md`, where the warning that
  a program theory is "not a list of API endpoints" could be misread as a rule
  to strip concrete taste anchors out of product theories.
- **Why it changed (pressure):** While crystallizing `enzan`'s program theory on
  2026-10-15, an agent flagged concrete CLI grammar and operation examples in
  `docs/program-theory.md` as potential BDUF to be moved out of the theory file.
  The owner corrected that framing: communicating the **feel** of a program
  (major verbs at the top level, `noun verb` elsewhere, core operations to build
  on) has been an intentional part of product program theories from the start
  across the ecosystem, and needed to be crystallized explicitly in
  `agent-theory`.
- **Evidence:**
  - *Owner-recalled:* Practice across prior product theories (`weft`,
    `simplebroker`, `engram`, `taut`) and explicit owner crystallization on
    2026-10-15.
  - *Contemporaneous:* `enzan`'s `docs/program-theory.md` (`[THEORY-3]`,
    `[THEORY-4]`, `[ALT-ENZ-009]`).

---

## Related documents

- `README.md` — Human overview of the discipline and this repository
- `docs/specs/02-agent-theory-and-program-theory.md` — Definitional primer
  explaining what Agent Theory and program theory mean
- `docs/specs/01-development-documentation-operating-model.md` — Normative
  process rules (`[DOM-2]` and `[DOM-3]` cover document roles and session
  startup)
- `docs/agent-context/` — Shared principles, decision hierarchy, and runbooks
- `skills/crystallize-program-theory/SKILL.md` — Owner interview, templates,
  and module-theory checklist
- `bin/bootstrap-agent-theory` — Installer that copies the process scaffold and
  a product-theory stub into another repository
