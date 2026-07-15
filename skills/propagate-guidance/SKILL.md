# Propagate Guidance to a Sibling Repository

Status: Active — pre-landing review passed 2026-07-14 (grok, two
rounds; see `docs/plans/2026-07-14-propagate-guidance-skill-plan.md`
§7).

**Hub-native: this skill lives only in agent-guidance and is not
scaffolded or copied.** Consumers receive waves; they do not push them.
The fresh-install counterpart is `bin/bootstrap-agent-guidance`; this
skill is the delta path for repos that already adopted the model.

## Purpose

Land a guidance wave (new spec sections, runbook additions, skills,
state files) in a sibling repository with SHA-pinned provenance, local
adaptation instead of clobbering, the receiving repo's own gates green,
a scoped independent review, and that repo's coalescing sweep — as one
unit of work. Distilled from the four 2026-07-14 landings (taut
`c09e95e`, backstitch `9ddb4d6`, engram `f92fa82`, weft `1e2e16d`) and
the review rounds that hardened them — defect → landing: anchor splice
(taut r1 wasn't needed; caught by taut's own scanner), six silent
omissions after script death (backstitch r1), wrong lessons derivation
+ missing transplants (backstitch r1), docstring numbering leftover
(engram r1), garbled blanket-replace prose + incomplete retargets
(weft r1), phantom foreign-plan cites (engram/weft), false-positive
content greps + script-tail commit (weft landing, self-caught).

## When To Use

- Any propagation of committed agent-guidance content into a sibling
  repo. Never propagate from an uncommitted working tree — pin the
  source SHA first (the 2026-07-02 fold's un-pinnable provenance was
  the original debt this rule exists to prevent).

## Governing Spec References

- `docs/specs/01-development-documentation-operating-model.md`
  [DOM-12]; [DOM-14] (the sweep-after-propagation standing rule lives
  in the coalescing plan and skill)
- `docs/lessons.md` 2026-07-14 entries: cross-repo git discipline;
  staging-safety rules

## Read First

- The receiving repo's `AGENTS.md` and agent-context read order — you
  are a guest; its decision hierarchy governs your work there
- `docs/lessons.md` 2026-07-14 entries (the staging-safety and
  cross-repo git rules this skill operationalizes). The four landings
  (taut `c09e95e`; backstitch `9ddb4d6`; engram `f92fa82`; weft
  `1e2e16d`) are worked examples spanning the divergence spectrum —
  read them in their repos when available, but this skill is
  self-sufficient without them

## Blast Radius

- The receiving repo's spec tree, agent-context, skills, plans index,
  lessons ledger, and state file — plus its own gates, which must be
  green before and after
- This repo: back-ported fixes when a landing exposes a canonical
  defect (three of four landings did)

## Workflow

### 0. Pin the wave and enumerate the payload

- Pin the **source SHA** (a committed agent-guidance state — never a
  working tree) and read the **consumer's last pin** (its lessons
  provenance note and/or state-file watermarks) — the wave is the delta
  between the two, not "everything I remember changing".
- Write the **payload checklist** into the propagation plan before
  touching anything: every spec section, runbook, runbook amendment,
  skill, state file, and pointer edit in the wave, one line each. This
  checklist is the recovery source when a transplant script dies
  mid-way (backstitch lost six transplants to memory-based resume) and
  the completeness gate afterward: grep-verify every line landed.

### 1. Survey — never transplant blind

Map, with commands not memory: the dirty tree (`git status`; classify
every dirty file as theirs/shared/absent from your targets); section
numbering (`grep -n '^## ' <principles, DOM spec>` — engram ran +1,
weft was fully re-numbered); lessons format (dated bullets vs dated H2
sections vs mixed — taut bullets, backstitch/weft H2); the plan-status
source (index table, `Status:` headers, or none); the runbook
inventory (weft lacked four canonical runbooks — every reference into
a missing runbook must be retargeted, not left dangling); whether a
DOM spec exists at all (weft: no — normative text then lands in
weft-idiomatic homes, not a new spec file); the repo's own gates
(taut: doc-reference tests; backstitch: mandatory zero-warning
self-corpus check; weft: `tests/specs/` including a plan-metadata
contract that will fail your plan file if its header block is wrong);
and the repo's **reference-code scheme** — canonical [DOM-N], a foreign
family, mixed, or none (weft, mm — beware lookalikes: mm's
`R-NNNN.NNN` codes are product risk-registry IDs, not doc codes).
Also survey: **where skills actually live** (a root `skills/` dir; or
`.agents/skills/` real dirs behind a tracked `.claude/skills/` symlink
layer — mm) and whether an external suite is **active** in the repo
(mm runs gstack), which turns the external-skill-suites crosswalk into
live routing that must match that repo's real skill inventory; whether
**any plan index exists at all** (mm: none across 535 plans); and
**locally numbered rule ledgers** (golden rules, testing patterns)
whose numbering diverges from canonical citations.

### 2. Write the propagation plan in the receiving repo

Dated plan, classified (these are 5+P where spec text lands, 3+P
effective 5 otherwise), carrying: source SHA; the receiving repo's
divergences and your adaptation for each; a dirty-tree invariant that
**names their WIP files** (and therefore poisons content-grep checks —
see step 6); the deviation log; the sweep as a task. Conform to the
receiving repo's plan-metadata contract exactly.

### 3. Transplant with heading-anchored inserts

- Extract payloads from this repo by regex on line-start headings;
  insert before line-start heading anchors with a **unique-match
  assertion** (`len(matches) == 1`). Never bare `str.index` — taut's
  scanner caught [DOM-14/15] spliced into the middle of a DOM-6 bullet
  because the anchor string appeared inline.
- **If the script dies mid-way, regenerate the remaining work from the
  payload list, never from memory** — the backstitch resume silently
  omitted six transplants and only the reviewer caught it. After any
  transplant run, grep-verify every payload landed.
- Local anchors drift: each repo's §10-equivalent had different coda
  text. Expect per-repo anchor fixes; assert loudly rather than skip
  silently. Minimal shapes:

  ```python
  ms = list(re.finditer(r"^## Anti-Patterns$", text, re.M))
  assert len(ms) == 1, f"anchor x{len(ms)}"   # never str.index
  ```

  ```bash
  # completeness gate: one grep per payload-checklist line
  for pat in "Plan Lifecycle" "Classify Before" "Retired-plan citation"; do
    grep -rl "$pat" <targets> || echo "MISSING: $pat"
  done
  ```

### 4. Adapt — the per-repo table

- **Status lines in copied skills cite the receiving repo's
  propagation plan and the source SHA**, never this repo's plan paths
  (path-claim scanners fail on foreign paths; engram/weft reviews both
  caught phantom cites).
- **Cite sections by name, not bare number, in portable text** —
  "engineering principle §12 (Enumerable Contracts Get Executable
  Gates)" — numbers are repo-local; two of four repos broke every bare
  §-reference. Where numbers are kept, mark them "this repo's
  numbering".
- **Blanket token replacement requires a readability pass.** A
  zero-leftovers assertion proves absence, not sense — weft shipped
  five garbled sentences past the assert; only review caught them.
- The state file owns the repo-local derivation commands (lessons
  format, plan-status source); the coalescing skill defers to it.
  Calibrate thresholds to ledger volume; document them as tunable.
- `bin/check-dom15-fixtures` negative-fact markers are repo-adapted by
  design — extend the marker list to the local phrasing; do not reword
  fixtures back to canonical brackets.
- Term collisions get explicit disambiguation where they live
  (engram: documentation-coalescing vs product memory coalescing).
- **No plan index at all** (mm: 535 unindexed plans): create a
  forward-only index with a declared boundary — "absence here is never
  a status claim" — and record backfill as the plans tier's
  reconsideration condition. Backfill is bulk-session work, never
  propagation work.
- **Numbered citations into forked ledgers must be re-derived per
  repo.** Golden-rule and testing-pattern numbers are repo-local; cite
  by name, or by number marked "this repo's numbering" after verifying
  it (mm's review round caught the hub's "Golden Rule 11, error path"
  pointing at their policy-cutover rule; theirs is 26).
- **Active external suites**: when the receiving repo actually runs a
  suite the crosswalk maps (mm: gstack), the crosswalk rows must match
  that repo's real skill inventory — drop rows naming absent skills,
  add present-but-unmapped ones, and say explicitly that the suite is
  active so the rows read as live routing.
- **Foreign code schemes get an explicit decision, recorded in the
  plan**: keep-foreign (cite their codes for their content), dual-cite
  ("[DOM-15]-equivalent, local code X"), name-map (name-based
  references, the weft pattern), or local-homes-only (no codes at all).
  Never silently renumber or restyle a repo's own code family — their
  traceability tooling and citations depend on it.

### 5. Gates — theirs, then ours

Run the receiving repo's own gates first (they caught defects mine had
missed in three of four landings), then the fixture checker, then any
canonical gates. A pre-existing baselined failure in their gates is
theirs — note it, never "fix" it in a propagation.

### 6. Scoped independent review

Different family, via `skills/call-agent/SKILL.md`, with the scope
fence stated verbatim: source content is already reviewed — review
ONLY the adaptation (placement, retargets, calibration, no-clobber,
performative additions). Capture the reviewer's full output to a file
before filtering or truncating it — the mm round lost findings 1–7 to
a `tail -c` on stdout and dispositions had to be reconstructed from
the verdict's own enumeration. Disposition per the review-loops handoff loop
in the receiving repo's plan. Round-2 verification is scoped to the
fixes; waiving a re-round for a verified one-line fix is legitimate
and must be disclosed in the plan.

### 7. Land — file-list staging, then commit, then pin

- Stage by explicit path list. For shared-dirty files, build synthetic
  HEAD+mine blobs (`git show HEAD:<f>` + your edits →
  `git hash-object -w` + `git update-index --cacheinfo`) so their WIP
  stays uncommitted.
- The gate is **staged-file-list equality** against the plan's expected
  list — content greps false-positive on your own plan's dirty-tree
  invariant (both backstitch and weft tripped this).
- **A failed check halts everything** — `if/else` around only the
  commit lets the script tail commit the full index anyway (the weft
  incident; recovered by `git reset --soft`). Structure the landing so
  nothing runs after a failed gate.
- Every git command names its repo (`git -C <repo>`); `git add -A` is
  banned where foreign WIP exists (per the 2026-07-14 lessons).
- Commit; then pin the state file's checked-through/source SHAs in a
  small follow-up commit (the source_sha pattern — the pin cannot be
  in the commit it names).

### 8. Sweep, back-port, report

- Run the receiving repo's first coalescing sweep in the same unit
  (standing rule). Before it: the state file must already declare the
  repo-local derivation commands, and any tier without a workable
  status source is recorded **not derivable** with its unblock
  condition — never guessed (at mm scale, ~534 plans, a guessed
  plans-tier count is fiction). An honest checked-deferred — with derived counts
  and reconsideration conditions — is a valid and often correct first
  sweep (weft: 57 sections and ~140 plans tripped; folding under time
  pressure destroys evidence).
- Back-port canonical defects the landing exposed (path-claim
  rewordings, marker extensions, portability fixes) to this repo and
  any already-landed siblings in the same session.
- Report per landing: commit SHAs, gates rerun, review verdicts and
  dispositions, sweep outcome, and any process defect honestly —
  including your own.

## Output Standard

- Receiving repo: propagation plan (dispositions populated), wave
  commit + pin commit, its own gates green, first-sweep run-log line,
  their WIP byte-identical to before
- This repo: back-ports committed; new lessons recorded if the landing
  exposed a reusable correction

## Maintenance Notes

- Each landing that hits a new divergence axis adds it to step 1's
  survey list and step 4's adaptation table in the same session.
- If two landings in a row need no adaptation beyond status lines, the
  ecosystem has converged — consider thinning this skill rather than
  growing it.
