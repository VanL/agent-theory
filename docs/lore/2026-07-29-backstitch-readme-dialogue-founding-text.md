# The backstitch README dialogue: founding text of the discipline's thesis (2026-07-29)

Status: Lore — curated primary-source excerpt; not normative guidance
Owner: repository owner
Boundary: Historical record. Nothing here binds work; the current
accounts live in this repository's program theory, in backstitch's
crystallization record, and in each product's own theory. The Naur
position quoted here was **revised by the owner on 2026-08-08** (see
the coda) — read this file as origin, never as the current claim.
Verification: Provenance below. Owner (USER) messages are verbatim and
complete; assistant messages are excerpted to their conclusions, with
elisions marked […]. The full stream remains recoverable from the
session log while it exists.
Required action: Read for origin context of the hub thesis sentence
("Delegate implementation, not understanding"), the possession
questions, and the iterative loop in the primer; and for the
identity material backstitch's program theory crystallizes. See
backstitch's plan "2026-08-08-program-theory-crystallization-plan"
(that repository) for the ratified current thesis.

**Source:** CCD session `local_c90d03d5-3e7e-4c3c-a576-f7b0f1f6b003`
("Backstitch code review"), working directory
`/Users/van/Developer/backstitch`, 2026-07-29, 142 messages.
Extracted 2026-08-08 via session-transcript retrieval during the
backstitch theory review. The session's first half is an eight-review
code audit (whose findings became backstitch's two completed
2026-07-29 remediation plans); the second half is the identity
dialogue extracted here. A full README draft ("v2", Naur-first,
analyze-centered) was produced at session end and never landed.

**Why kept:** this dialogue is where the discipline's thesis sentence
entered the working record — one day before the hub's program-theory
docs landed carrying it — together with the nine possession
questions and the iterative loop that became the primer's
[AT-REF-4]. Until this extraction, the founding text existed only in
a session log no repository surface referenced: the
refusals-don't-transfer failure mode operating at the theory tier,
about the theory itself.

**Authorship correction (2026-08-08):** the thesis sentence, the nine
questions, and the iterative loop were **not minted by the owner in
this dialogue**. The USER message quoted in §2 is a composite: the
owner's own words up through the practice description, followed by
pasted text from an external naming conversation in which **another
agent** coined the sentence in reply to the owner ("**Your** method
re-establishes the coupling… Delegate the implementation, not the
understanding" — words addressed *to* the owner). Evidence: the
naming-conversation transcript preserved in the hub session log
shows the sentence ~7.8k characters after its `Response:` marker,
inside the other agent's reply. The owner stated the practice and
the risk diagnosis; the external agent compressed the practice into
the sentence; the owner recognized it as true and adopted it. That
order is itself an instance of the practice-first admission test:
the naming came second, and not from the practitioner.

---

## 1. The owner's framing of the task

**USER** (opening the identity work, after the audit):

> Getting from 0 to 1 with backstitch has been harder than expected,
> but I think I am about at alpha. What I want to start doing is
> reworking backstitch to improve its quality.
>
> But the very first thing to do is to explain what backstitch *is*,
> and why. Part of that is what I want to work with you on.
>
> You are probably familiar with Peter Naur's "Programming as Theory
> Building" - the process of programming is defining and
> communicating a theory about the problem being defined and the way
> in which we solve it. The spec-driven-development setup in
> backstitch is part of what I am developing as agent-theory: How to
> interactively explore and develop the theory of the software as
> part of agent-assisted development.
>
> Backstitch is both a recipient of that and one of the ways in which
> I am working to formalize working with agents. But I need to start
> by creating the best README I can about what backstitch is for and
> why.

And, restated:

> Stated another way, I would like you to explore with me how to
> communicate in the README the vision of backstitch to both humans
> and agents.

## 2. The founding text

The assistant put three positions on the table (the hourly-theory-
death reading of Naur; agents needing *more* decision-shaped "why"
than humans because there is no apprenticeship for agents; the
backstitch name as the compressed thesis). The owner's reply is the
founding text as it entered this repository's lineage — a composite
message: the opening ("You are partly right…" through the practice
description) is the owner's; from "The real risk in agent-assisted
development…" onward it is pasted from the external naming
conversation, where it was the *other agent's* reply to the owner
(see the authorship correction above):

**USER** (verbatim and complete as sent; composite authorship):

> You are partly right about the third answer, but in a real sense,
> agent-theory is a bet that computerized intelligence, relentlessly
> focused on specification (intent) + code + tests, can do what Naur
> said was impossible: iteratively and collectively develop the
> theory of the software, with the actual code being just a part of
> the story. It is also akin to Knuth's literate programming, but
> with separate files.
>
> Agents are very good at maintaining documentation - better than
> humans. They are good at reading documentation - better than
> humans. They are also good at complying with gates. Backstitch is
> about tying meaning to code in a reproduceable, 'executable gate'
> type of fashion.
>
> One reason I like agent theory is also because one of the core
> issues that people keep raising regarding agent-assisted
> development is that 'outsourcing' the thinking to the agent leads
> to a codebase that is brittle, sloppy, and that the human cannot
> understand or reason about. In contrast, the way in which I have
> been operating - not big design up front, but developing a concept
> and then iteratively developing a specification (with associated
> docs and code) that refines and builds on that concept has
> personally kept me both involved and has made it so that I have
> probably as good a working understanding of the codebase as when I
> wrote each line myself.
>
> The real risk in agent-assisted development is not that the agent
> typed the code. It is that implementation becomes decoupled from
> human understanding. Historically, writing and debugging code
> forced the developer to acquire at least some working theory of the
> system. Agents remove that friction. A human can now request a
> feature, receive a plausible implementation, run the tests, and
> merge it without ever developing a model of why the system has that
> shape.
>
> Your method re-establishes the coupling at a different and arguably
> higher-leverage surface:
>
> Delegate the implementation, not the understanding.
>
> The human does not need to choose every variable name or write
> every branch to possess the theory of the program. The human needs
> to understand:
>
> * What concepts exist.
> * What each concept means.
> * Which component owns each behavior.
> * Why the boundaries are where they are.
> * Which alternatives were rejected and why.
> * What must remain invariant.
> * What the system explicitly does not do.
> * How a proposed change affects the rest of the model.
> * What evidence would show that the current understanding is wrong.
>
> That is the intellectual work. Line-by-line coding is one
> traditional way to perform it, but it is neither necessary nor
> sufficient. Someone can write every line while accumulating only
> local implementation knowledge and a weak theory of the whole.
> Conversely, someone can understand a system deeply without
> personally typing most of it, provided they participate in the
> decisions, interrogate the implications, inspect the realization,
> and reconcile surprises back into the shared model.
>
> This is not big design up front
>
> That distinction is important because "specification-driven" can
> easily be mistaken for waterfall development.
>
> What you are doing is closer to iterative theory building:
>
> initial concept → questions and alternatives → provisional
> specification → implementation → evidence and surprises → revised
> specification and theory
>
> The specification is not an advance decree produced before
> discovery begins. It is the current best articulation of what has
> been discovered.
>
> Implementation remains epistemically important. It puts pressure on
> the theory:
>
> * A proposed abstraction may turn out not to fit the actual
>   dataflow.
> * A supposedly local feature may reveal a hidden identity or
>   lifecycle problem.
> * A test may show that two concepts the spec treated as equivalent
>   are different.
> * A platform failure may expose an unstated environmental
>   assumption.
> * A review may show that two plausible implementations encode
>   different product semantics.
>
> Those discoveries flow back into the theory. That is why the
> associated specifications, implementation rationale, plans, tests,
> and lessons all matter. They are not paperwork surrounding the
> code. They are the surfaces through which understanding is created,
> challenged, and retained.

## 3. The dialogue's products (assistant conclusions, excerpted)

On the corpus-substrate reading of the bet:

> […] the bet isn't "agents can do the impossible." It's that
> **theory can live in a corpus rather than in a team**, provided
> something keeps the corpus honest. And that proviso is the whole
> tool. An unreconciled spec isn't a weaker theory; it's a *false*
> one, and false theory is worse than absent theory because it's
> confidently wrong in exactly the way a new session will trust. […]

On the Knuth lineage and its cost:

> […] **separate-file literate programming without a gate is just
> documentation, and documentation rots. The gate is what makes the
> separation survivable.** […]

On the nine questions as product spec (with the honest coverage
finding — three gated, three partial, three prose-only):

> […] Non-goals and rejected alternatives are the parts of a theory
> that *only* survive in prose today and that agents most reliably
> violate, because an absent constraint is invisible […]

On the loop's weak joint:

> […] Agents are agreeable and locally competent, which is precisely
> the profile that absorbs a surprise instead of reporting it […]
> A suppression is a *recorded* surprise […] Requiring a spec
> declaration and a rationale is what converts a swallowed surprise
> into a reviewable one.

Later in the session, after the owner's corrections ("agent-theory
[the hub] will be the true home of the concept"; "your README helps
with the mechanical part, but doesn't emphasize the analysis part —
that is what wasn't possible before"; intent-coverage direction), the
dialogue also produced: the `ambiguous`-verdict reading (check proves
the theory well-formed, analyze proves it true, `ambiguous` maps
where it is under-articulated); the two-tool division (backstitch
asks whether the theory is still true of the code; an erosion tool —
decomplex, "an experiment" — asks whether the code is still capable
of having a theory); and the theory-shape projections
(reach/scatter/concentration), whose fan-in count independently
reproduced the architecture review's two grab-bag modules.

## 4. What became what

| Dialogue product | Where it landed |
|---|---|
| "Delegate the implementation, not the understanding" (external agent, adopted by owner) | Hub `README.md` thesis line; [AT-REF-1] central claim |
| The iterative loop (external agent, adopted by owner) | Primer [AT-REF-4] |
| The nine possession questions (external agent, adopted by owner) | Compressed into the primer's possession criteria and [AT-THEORY-6] possession probes; full list promoted 2026-08-08 into the crystallize skill's §7 confirm step as the owner's checklist |
| "Agents comply with gates" (owner) | Engineering principle §12's rationale ("agents comply uniformly with gates and unevenly with everything else") |
| Hub-as-true-home + backstitch-as-instrument (owner) | Hub identity; backstitch crystallization rung 1 |
| Corpus-substrate reading; claims-vs-contracts; hourly theory death; stitch image; nine-questions status table; README v2 draft | **Never landed** — preserved here; disposition owned by backstitch's crystallization (rungs 3–6) |

## 5. Coda: the 2026-08-08 revision

During backstitch's theory crystallization the owner revised the
founding position — a demotion-in-place of the "do what Naur said
was impossible" framing:

> On 1, I am not sure that I am arguing for falsification of Naur
> anymore. I think that his strongest claim - that the theory lives
> in people's heads (or agent's context) is still true, maybe
> tautologically so. Instead, the idea has changed to the concept
> that automated intelligence allows for repeatable evaluation that
> some portion of a theory is exposed through particular code.

The ratified current thesis lives in backstitch's crystallization
plan (decision D1, that repository) and, once crystallized, in
backstitch's `docs/program-theory.md`. This file records where the
thesis came from; it does not state it.
