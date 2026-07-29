# Guidance Gates: Self-Checking the Corpus

Status: completed
Class: 3+P — executable tooling for the guidance repo plus two normative
one-liners; process-material (the gates change how landings are
verified), hence +P: independent review before completion. Hardening:
N/A — no risky trigger (tooling + docs; the bootstrap change is
create-time only and covered by a scratch-scaffold test).

Origin: the 2026-07-28 external review (three-stage: shallow → full-read
→ field audit of four consumers). Its surviving findings, verified
locally before acceptance: (1) the bootstrap ships hub-plan path
citations verbatim — five scaffold files carry paths that exist only in
the hub (the phantom-cite class the delta path already fixes by rule);
(2) the generated lessons ledger lacks the Golden Rules section three
pointers direct agents to; (3) the source_sha cue contract is the most
load-bearing unchecked prose in the system — and the field audit showed
cues additionally break across the publication boundary (local SHAs not
resolvable in published mirrors); (4) the session-start trigger check
leaves no evidence trail; (5) the pilot gate for the coalescing layer
closed with criterion 4 (measured context savings, retrieval friction)
unevaluated.

## 1. Deliverables

1. **Bootstrap adaptation layer** (`bin/bootstrap-agent-theory`): a
   provenance-rewrite pass applied to copied guidance files at scaffold
   time — hub plan paths become quoted foreign names, and each rewritten
   file gains an installed-from provenance line pinning the hub HEAD at
   scaffold time. Same transformation `propagate-guidance` §4 mandates
   for waves; the fresh-install path finally learns the delta path's
   rule. Plus: the generated `docs/lessons.md` gains its Golden Rules
   section (empty, with the promotion note), matching the three pointers.
2. **`bin/check-doc-paths`**: every backticked repo-relative path claim
   (`docs/…`, `skills/…`, `bin/…`) in the guidance surfaces must resolve
   — run against the tree, and with `--scaffold` against a fresh scratch
   scaffold. Wired into landing gates beside `check-dom15-fixtures`.
3. **`bin/coalesce-check`**: derives the tier counts per the state
   file's documented commands; verifies every run-log `source_sha`
   resolves (`git cat-file -e`) and every `git show <sha>:<path>` cue
   grep-resolves at that SHA; checks each SHA against the published
   remote where one exists, reporting `local-only pin` — the cue
   contract becomes checked prose, and a session-start invocation gives
   the read-only check a quotable evidence trail without write authority.
4. **Normative one-liners** (owner-approved wording): the harness
   scoping sentence beside the AGENTS.md overrides (harness controls are
   outside the hierarchy — not above it, simply not guidance); the
   cue-portability rule in the coalescing skill's cue guidance (cues
   resolve in published history where a mirror exists, else the run-log
   line marks `local-only pin`).
5. **Pilot-gate debt record**: a dated run-log line in
   `docs/coalescing.md` recording that the 2026-07-14 coalescing-layer
   pilot gate's criterion 4 was never measured — the closed plan is
   immutable, so the correction is a new record, not a retro-edit.

## 2. Verification

- `check-doc-paths` exits 0 on the tree AND on a scratch scaffold
  (proving the adaptation layer closed all phantom citations); a
  deliberately broken path makes it exit 1 (firing test).
- `coalesce-check` exits 0 on the hub state file; a deliberately
  corrupted SHA makes it fail (firing test); its local-only detection
  demonstrated against the current unpushed state.
- Scratch scaffold greps: zero hub plan paths; `^## Golden Rules`
  present in generated lessons.
- Existing gates stay green: `check-dom15-fixtures`, backstitch
  self-corpus 0/0/0.

## 3. Review

Per +P: scoped independent review (different family) of the diff before
completion; dispositions recorded below.

### Dispositions

Scoped review (grok, read-only, 2026-07-28; §4a-form brief). Round-1
verdict: **blocker: F1, F2** — both fixed same pass; re-verified: tree
and `--scaffold` modes exit 0, adapted output prose clean, firing tests
fail correctly.

| ID | Sev | Finding (gist) | Disposition |
|----|-----|----------------|-------------|
| F1 | P1 | The new cue-portability paragraph hard-claimed `bin/coalesce-check` — a hub-only path that fails the scaffold scan; the unit's own new gate caught the unit's own same-pass edit | **Fixed:** soft reference ("where a coalesce-check tool is installed"), matching the skill's existing pattern |
| F2 | P2 | Raw-string escape left a literal backslash in every adapted consumer file ("repository\\'s") | **Fixed:** non-raw replacement string; scaffold output verified clean |
| F3 | P3 | `resolve_anywhere` accepts a bare wrong-repo SHA that happens to exist in a sibling | **Accepted with eyes open:** honest for the state file's multi-repo cells; tightening to required repo tags is future work if bare-SHA abuse appears |
| F4–F5 | P3 | (minor tool semantics; remote-branch assumption) | **Accepted;** revisit if a consumer uses a non-main default branch |
| F6 | P3 | Plan-path regex year-pinned to 2026 | **Fixed:** `[0-9]{4}` |
| F7 | nit | Correction line said "criterion 4" for two criteria | **Fixed:** "criteria 3–4" |
| F8 | nit | "Wired into landing gates" is prose-wired, like check-dom15-fixtures | **Accepted:** consistent with the existing gate's wiring; mechanical CI wiring is a separate decision |
| F9 | nit | Provenance insertion silently skipped for titleless files | **Accepted:** all current sources titled; EOF-fallback if a titleless source ever appears |

Reviewer observations recorded: the local-only detector is logically
correct but unexercised by current state (no cited SHA is unpushed);
`bin/__pycache__` stays out of the commit; provenance pins HEAD while
scaffolding worktree content — accurate once landed as one commit.

## 4. Out of Scope

- ~~Propagating the tools to consumers (next wave; coalesce-check needs
  per-repo derivation adaptation there).~~ **Closed:**
  `bin/check-doc-paths` and `bin/coalesce-check` joined
  `bin/bootstrap-agent-theory` `COPIED_FILES` alongside
  `bin/check-dom15-fixtures` (consumer lessons-tier derivation remains
  the dated-bullet default; repos with other ledger formats still adapt).
- The per-task instrumentation log (owner call, open).
- Pushing any remote (owner's publication discipline decision).
- [DOM-14] spec text changes (the cue-portability rule lands
  skill-level; spec promotion follows the normal gate if a second
  lineage or owner direction arrives).
