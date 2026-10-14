# Naur / Ronacher / Yegge–Gas Town discussion (grok session, 2026-07-30)

Status: Lore — curated primary-source excerpt; not normative guidance
Owner: repository owner
Boundary: Historical record. Nothing here binds work; promoted conclusions
live in the hub program theory and its plan.
Verification: Provenance below. Owner (USER) messages are verbatim and
complete; reviewer (GROK) messages are excerpted to their conclusions, with
elisions marked `[…]`. The full unedited stream remains recoverable from
the source below while it exists.
Required action: Read for origin context of `[AT-THEORY-4]`–`[AT-THEORY-6]`
and the module-theory doctrine; see the companion note
`2026-08-08-gastown-prediction-confirmed.md` for what happened next.

**Source:** grok session `019fb2b4-78e2-70d0-a534-97ec4fbb31df`, working
directory `/Users/van/Developer/simplebroker`, 2026-07-30. Extracted
2026-08-08 from the session's `updates.jsonl` under `~/.grok/sessions/`
(the session's own `chat_history.jsonl` was truncated by grok-side
compaction; the update stream is complete). Messages [20]–[40] of 186;
earlier messages are a simplebroker product audit, later ones return to it.

**Why kept:** this session is where surprise-as-collapse-signal, the
possession loop, the Gas Town contrast, the speed-vs-theory fit rule, and
module-theory-as-extension were first worked out. Its only prior record was
an unversioned, compaction-lossy file in `~/.grok`; it survived two failed
retrieval attempts before this extraction.

---

## 1. The contrast that started it


**USER [20]:**

*I* don't have "A sibling product of similar difficulty built with “just agents + README + tests”". That doesn't mean it doesn't exist. The first extraction in April came from people asking why my agents 'seemed smarter' than theirs even though we were using the same models+harnesses. Part of what is driving the recent crystallization is contrast with this article by Armin: https://lucumr.pocoo.org/2026/7/13/the-tower-keeps-rising/


**USER [22]:**

Part of what I am also experiencing - although this is 'vibes' - is that using this method has enabled me to maintain the theory of each program in *my* head as they have been developed - subjectively, about as well as when I wrote all the code myself.


---

## 2. The possession loop

**USER [24]:**

Strongest personal signal: When something happens in the program that I don't expect, or when I see an agent 'thinking' about something that I don't expect, it forces me into "What about my mental model is incorrect in the face of this evidence?" This has been true for both bugs highlighted by external uses/pressures as well as agent-typical process failures (duplicate code paths, mixed boundaries, etc). I think about process coordination a lot more than I did previously. A lot of the development of agent-theory was an attempt to force agents not to go down paths that didn't make sense (global vs local knowledge). What is driving the current program-theory.md development is the realization that I kept on asking agents to "Read the README and specs so that you get an idea of the type of product that we are making, before we talk about a new feature." We would then discuss 'simplebrokerness' or 'weftness' or 'tautness' in the context of a feature or implementation. I realized that this was me trying to orient the agent into the theory of the program.


**GROK [25]** (excerpt):

That history makes the whole stack snap into focus. You’re describing a **closed loop for theory possession**, not a documentation hobby.

---

## The signal that actually matters

Unexpected **program** behavior *or* unexpected **agent** behavior →  

> “What in *my* model is wrong, given this evidence?”

That is Naur’s possession test in the wild:

| Event | Bad response | Your response |
|-------|--------------|---------------|
| Bug / external pressure | Patch the symptom | Revise the mental model |
| Agent digs a nonsense path | Re-prompt harder | Ask what boundary/global knowledge was missing |
| Mixed boundaries, duplicate paths | “Agents are messy” | Process failure as **theory or transfer** failure |

Two sources of surprise, one discipline: **evidence updates the theory**, not only the code. Agents become sensors for holes in *your* model and in the **shared language** you thought you’d externalized.

That also explains why you think more about **process coordination** now. Under agents, “local reasonableness” is cheap. The scarce skill is keeping **global product identity** (simplebrokerness / weftness / tautness) binding on local work—the global vs local knowledge problem agent-theory was built to constrain.

---


*[…]*


**Armin:** agents let the tower rise without shared language; no immediate collapse.  

**Your loop:** surprise *is* the collapse signal—when you or the agent behave outside the model, you treat it as **model error**, not noise. That reintroduces pain and synchronization that pure vibecoding skips.

**Naur:** theory is shown by diagnosis and coherent change under new demand.  

**Your practice:** bugs and agent-typical failures are both demands on the theory. Process failures (duplicate paths, mixed boundaries) count because they mean the **transfer** of theory into executable work failed—not only that Python was wrong.

“About as well as when I wrote all the code myself” then means: you still **own the revision loop**. Agents write text; **you still update the theory when the world disagrees.** Solo coding forced that via every keystroke. This method forces it via **orientation + refusal + surprise-as-evidence**.

---


---

## 3. The Gas Town question

**USER [26]:**

Here is an interesting case: take a look at Steve Yegge's gastown (you can find descriptions + a public repo). GT is built with an explicitly different protocol, one that is much more hands-off. In the case of gt, I think Yegge did have a Naur-style theory that has been developed over time. You can look at some of his writing and see it. The question is - does the code itself faithfully represent the theory of the program that is Yegge's head? Do we have evidence that Yegge possesses (or still possesses) a clear theory of the program? Does the gt code show conceptual unity?


**GROK [27]** (excerpt — from essays + public repo surface, pre-clone):

## 1. Does Yegge have a Naur-style theory?

**Yes—strongly, and it is externalized in prose more than in product-contract form.**

The launch essay is not a feature list. It is a **theory of multi-agent work at scale**, developed over failed orchestrators (v1 throwaway → v2 → Beads → Python Gas Town → Go Gas Town) and earlier public prediction (“Kubernetes for agents,” multi-level supervision, merge queue).

Stable conceptual spine:

| Idea | Content |
|------|---------|
| **Problem** | One agent is a camel; the next form factor is lashing many together (throughput, not IDE polish) |
| **Unit of work** | **Beads** = git-backed sticky-note work graph (not “memory in the chat”) |
| **Session vs agent** | Sessions are cattle; **agent identity is a bead** (persistent) |
| **GUPP** | If work is on your hook, you **must** run it (physics over politeness) |
| **MEOW (as he defined it)** | **Molecular Expression of Work**: beads → epics → molecules → protomolecules → formulas → “guzzoline” |
| **NDI** | **Nondeterministic idempotence**: path may wander; durable molecules + restarts aim at *eventual completion* (not Temporal’s deterministic replay) |
| **K8s contrast** | K8s: “is it running?” / Gas Town: **“is it done?”** |
| **Human role** | Overseer / PM / idea compiler; tolerate slop for velocity |
| **Operating regime** | Stage 7–8 only; expensive; chaotic by design (“fish fall out of the barrel”) |

That is a real working theory: problem → concepts → ownership (who is cattle, what is durable) → propulsion (GUPP) → completion model (NDI/convoys). It is **Yegge-shaped**: metaphor-heavy, throughput-first, anti-politeness, opinionated data plane (Beads only).

So: **theory exists and evolved.** It is closer to a **manifesto + runtime mythology** than to your `program-theory.md` + gated product specs.

---

## 2. Does he still *possess* that theory?

**Mixed—and he is unusually explicit about a non-Naur relationship to the *code*.**


*[…]*


### Evidence that possession of the *implementation* theory is weak or declined

He says it out loud:

> Gas Town is 100% vibe coded. **I’ve never seen the code, and I never care to**… same for Beads (then cited as ~225k LOC).

In Naur terms that is almost a **confession of non-possession of the program-as-code**. He may still possess:

- the **product idea** (factory of agents, Beads plane, GUPP), and  
- the **operator’s theory** (how to wrangle chimps),

while **not** possessing:

- module ownership,  
- why a particular Go package exists,  
- how edge cases in merge/refinery/daemon interact,  
- the ability to diagnose a bug without another agent.

Naur’s possession is *practical*: place change, diagnose surprise, revise coherently. Yegge’s protocol optimizes for **throughput of work through agents** and treats **code as disposable medium**. Those can coexist with a strong *product* theory and a thin *code* theory.

**Emergency manual vibe:** “idle polecats” and heresies keep re-entering codebase/docs; fix is **agent priming**, not “I read the implementation and tightened the model.” That is theory-as-**prompt culture**, not theory-as-**code fidelity**.

**Verdict on possession:**  
- **Clear theory of Gas Town as a *system of work***: yes.  
- **Clear theory of Gas Town as a *coherent program text***: he claims no, and the protocol does not require it.  
- Whether he *could* still reconstruct implementation theory under pressure is unknown; he has chosen not to make that the success criterion.

---


**USER [28]:**

If you need to you can clone locally


**GROK [29]** (excerpt — after cloning the repo):

## Updated answers to your four questions

1. **Naur-style theory developed over time?**  
   **Yes.** Confirmed in essay + glossary + architecture + ZFC + GUPP/NDI/MEOW (molecular). Evolved through Beads → molecules → patrols → convoy → more.

2. **Code faithfully represent theory in his head?**  
   **Partially.** Major roles and Beads/GUPP are embodied. **Not faithfully** as a single consistent conceptual inventory (MEOW split, ZFC vs hard GUPP timeouts, doc workflow versions, package accretion). Faithfulness is to **runtime completion physics**, not to a frozen conceptual model.

3. **Evidence he still possesses a clear theory of the program?**  
   - **Of the factory / work physics:** yes (and the repo still teaches it).  
   - **Of the Go program as one theory object:** weak; protocol and his statements optimize for **not needing** that. Community PRs + shallow AGENTS path reinforce **distributed** implementation knowledge.

4. **Conceptual unity of GT code?**  
   **Moderate skeleton, low–moderate overall.** Skeleton: beads two-level, roles, propulsion, refinery-as-completion. Body: acronym collision, doctrine violations, 70 packages, dual docs. Unity is **myth + operational spine**, not **tight concept inventory**.

---

## Contrast with your method (sharpened by local evidence)

| | **Gas Town** | **Your stack** |
|--|--------------|----------------|
| Where theory lives | Essays, glossary, prime/templates, scattered `// ZFC`/`GUPP` | Specs + program-theory + gates |
| Contradiction handling | Can ship dual MEOW on main | Surprise / agent path → “what’s wrong in *my* model?” |
| Cognition locus | Explicitly agents (ZFC); Go still sneaks cognition | Human theory-owner; agents implement under X-ness |
| Scale signal | ~250k non-test LOC, multi-author swarm | Smaller products, denser contracts |
| Success metric | Town keeps completing work | Human still holds product theory |

Gas Town is the interesting opposite: **rich public theory of orchestration** + **hands-off implementation protocol** that *does not require* the human to feel implementation surprise as model error. Your method treats that surprise as the main instrument.

The local clone does **not** show GT as “theory-less vibecode.” It shows **theory-full vibecode**: a strong operational mythology that generates a large machine faster than the shared language can stay single-valued—MEOW being the exhibit A, ZFC-vs-timeouts exhibit B.

---

**Clone path:** `/tmp/gastown` (shallow). I can delete it or dig a specific subsystem (refinery, formula cook, prime injection) if you want a still tighter “does package X match concept Y?” pass.


---

## 4. MM as the sharper comparison

**USER [30]:**

Here is a sharper comparison: Look at ../mm. MM doesn't have the full agent-theory. Like simplebroker, it was one of the primary places where it was developed. It is a large, complicated system with multiple developers and concurrent work with agents. Parts of agent-theory were organically evolved there, and it (along with weft) were the two repos that were used to extract the first formalization of agent theory (as agent-guidance).


**USER [32]:**

Examine/compare/contrast the quality of MM and GT. Is agent-theory buying 'quality'? Shipping speed to usable product (i.e., not just pushed, but relatively usable and bug free)? Conceptual clarity? (I think MM would win there, as that is part of what I am optimizing for, but an outside evaluation is helpful.) Maintainability?


**GROK [33]** (excerpt):

## Synthesis: what is actually being optimized?

```text
MM  →  identity-preserving evolution of a multi-human SaaS
       under agents  (agent-theory lineage)

GT  →  completion-preserving evolution of a multi-agent factory
       under vibecode  (ZFC / GUPP lineage)
```

| If you score… | Winner | Agent-theory’s role |
|---------------|--------|---------------------|
| Conceptual clarity of **product** | **MM** | Central |
| Maintainability of **shared product** | **MM** | Central |
| Usable **customer** product | **MM** | Contributing, not sole |
| Speed to **powerful** multi-agent setup | **GT** | Peripheral / alternate |
| Usable **for non-experts** | **MM** | Helps orientation |
| Hands-off code possession | **GT** | Opposite philosophy |
| Bug-free in absolute terms | Neither claims it; MM aims higher for product bugs | Filter, not guarantee |

---


---

## 5. The value question

**USER [34]:**

Real world: Which leads to more value? Absolute speed + slop tolerance, or theory maintenance with agentic dev?


**GROK [35]** (excerpt):

## A simple decision rule

```text
If (multiple humans OR external users OR long life OR hard invariants)
   AND agents are a large fraction of edits:
     → theory maintenance usually wins on net value

If (solo/tiny OR exploratory OR short life OR frozen contracts OR pure bulk):
     → speed + slop usually wins on net value

If both pressures are high (MM):
     → hybrid: theory on the identity surface, speed inside bounded slices
```

MM is the hybrid under stress: you invent process **because** multi-dev + agents + real product force it. GT is pure speed pole under Stage‑8 and optional code non-possession.

---


*[…]*


## Direct answer

**More value overall, for durable multiplayer products under heavy agent use: theory maintenance.**  
That’s the scarcer bottleneck once models make raw coding cheap; Armin’s tower is the failure mode of pure speed; MM is the existence proof of value under concurrency.

**More value for solo exploration, personal factories, and short-horizon leverage: absolute speed + slop.**  
GT is the existence proof; denying that is ideology.

**Most real-world portfolios should run both:** theory on what must stay true across minds and time; speed on what is disposable or contract-bounded. Agent-theory is not anti-speed—it is **where you refuse to spend speed**: on redefining the product by accident.

If you only optimize one in an agent-dense 2026: **bias toward theory maintenance for anything you will still own in a year with more than one writer.** Bias toward speed+slop for anything you will throw away or only you will ever steer.


---

## 6. Module theory enters

**USER [36]:**

Take a look at /Users/van/Developer/mm/apps/registry/MODULE-THEORY.md


**GROK [37]** (excerpt):

## One-line characterization

`MODULE-THEORY.md` is **Naur program theory for one MM module**: ownership, non-goals, a single generative model (control locality), design consequences, falsifiers, and decision cases—written so an agent can enter `apps/registry` without the whole monorepo theory, and so “simplebrokerness”-style **registry-ness** is enforceable under multi-agent crosswalk work.

It is also a live demo of your method’s core claim: **the high-value step is orienting (and revising) the theory before changing the inventory**—here, literally “read this before changing a class, domain, pattern, scope boundary, or assignment rule.”


**USER [38]:**

We needed to help agents work with the registry, but this is local knowledge only applicable to risk registry work, so I didn't want to put it at top level, as it would make program-theory.md too verbose. This is my attempt to extend the model for MM.


**GROK [39]** (excerpt):

## What you are extending

The full ladder is roughly:

```text
agent-theory (process: how we keep theory alive)
        │
product program theory (MM-wide: what Model Monster is / is not)
        │
module theory (apps/registry: what the risk registry is / is not)
        │
contracts / fixtures / code (exact rules, inventory, behavior)
```

**Problem:** Registry work needs deep global-for-the-module knowledge (control locality, Class 4 admission, counterfactual, ALT refusals). That is **not** product-wide “model-monster-ness.”

**Wrong fix:** Stuff it into product `program-theory.md` → every agent on billing/UI/auth pays a registry tax; product theory becomes a junk drawer.

**Your fix:** Second rung, **on entry to the module only**, written so it does not require sibling module theories ([REGISTRY-0]/[REGISTRY-1]). Local knowledge stays local; progressive disclosure stays progressive.

That matches Naur + agent-theory:

- Theory is what you need to **place work coherently**.  
- Different work needs different theory **granularity**.  
- Agents fail on **global vs local** when local knowledge is missing *or* when local knowledge is shoved into the global packet.

---


*[…]*


## Bottom line

Your attempt extends the model correctly:

> **Program theory is progressive disclosure by ownership scope.**  
> Product theory orients “what kind of product.”  
> Module theory orients “what kind of subsystem,” only when you enter it.  
> Contracts hold exact rules.  
> Process (agent-theory) keeps the ladder alive under multi-agent multi-dev load.

`MODULE-THEORY.md` is local knowledge in the right place—with explicit non-goals for the document itself (what it does not contain), which is the same discipline applied one level down. The open debt is finishing the **product** rung so registry does not remain the only fully Naur-shaped theory file in MM by accident.


---

## 7. The pivot into the hub

**USER [40]:**

Right now you have a lot of context on agent-theory and program-theory. None of this is represented in the hub yet (../agent-theory/). We may change things, but I would like to capture a first draft of agent theory as a theory, including references to Naur, Ronacher and  Knuth's literate programming. I would like you to include a program-theory.md in the agent-theory repo that is the program theory for what agent-theory is, and how it can be maintained and extended, generalizing from what you see in SB and MM (but without naming those repos). The program-theory should have an explicit note that it should be replaced in each repo, and maybe even there should be a set of questions or a skill (like a grill-me) that helps users crystallize their program theory. (https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md)

Also edit the README. Should be similar, with the understanding that the README is for humans and the program-theory.md is for agents. Note that we actually have a copy of the Naur article here: /Users/van/Downloads/1985-naur.docx.md


*(The session then drafted the hub's `docs/program-theory.md`, the
module-theory extension rule, and the crystallize skill — the work recorded
in `docs/plans/2026-07-30-program-theory-and-module-theory.md`.)*
