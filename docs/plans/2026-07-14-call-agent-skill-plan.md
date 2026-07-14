# Call-Agent Skill Plan

Status: Draft — awaiting pre-landing independent review (+P requirement)
Class: 3+P (effective 5) — a new reusable skill ([DOM-5] non-trivial
trigger: reusable workflow) that is [DOM-6]-material to how future work
is reviewed. Spec delta: none required — [DOM-11] (independent review)
and [DOM-13] (agent availability) already define the contract; this
skill operationalizes invocation mechanics that no spec or runbook
currently owns. The pre-landing reviewer is invited to challenge that
declaration. Hardening: N/A — no [DOM-5] risky trigger fires.

## 1. Goal

Own the mechanics of invoking a second agent family for independent
review, so the [DOM-11] review loop stops depending on the agent-mcp
MCP server (fragile: node process, session-attached, absent in
headless/cron runs) or on vendor skill suites (the gstack codex wrapper
runs ~700 lines of telemetry and onboarding around a one-line CLI
call). One repo-owned skill, six usable agent families (plus a
deprecated gemini row and an antigravity placeholder — see §8),
read-only review posture by default.

## 2. Source Documents

- `docs/specs/01-development-documentation-operating-model.md`
  [DOM-11], [DOM-13], [DOM-15]
- `docs/agent-context/runbooks/review-loops-and-agent-bootstrap.md`
  (reviewer inputs, prompt, handoff loop — this plan adds mechanics,
  not policy)
- `docs/agent-context/runbooks/external-skill-suites.md` (harvest
  justification: the codex invocation fired four times on 2026-07-14
  and its findings shaped three plans and a spec section — citation
  evidence per the crosswalk's maintenance rule)
- Harvest sources, validated not copied: `../agent-mcp/src/server.ts`
  provider adapters (flag tables), the gstack codex skill's operational
  hardening (timeout wrappers, stderr capture, non-zero-exit surfacing,
  known-bad version list), and live `--help` verification of the
  installed CLIs (2026-07-14).

## 3. Context and Key Files

- New: `skills/call-agent/SKILL.md` (lands with this plan, Status:
  Draft until review passes).
- Post-review wiring (promotion step): one pointer line in
  `review-loops-and-agent-bootstrap.md` §1 (that runbook owns *policy*
  and currently names no invocation mechanics — one-owner routing, not
  sprinkling); one crosswalk row update (gstack codex remains valid
  when present; this skill is the dependency-free path); COPIED_FILES
  entry; `docs/implementation/03-agent-inventory.md` refreshed via the
  skill's probe procedure.
- Read first: the agent inventory doc (currently a stub in this repo —
  the probe procedure is what fills it), review-loops §3–§5.

## 4. Invariants and Constraints

- **Review posture is read-only, and only OS-enforced sandboxes count
  as verified containment.** agent-mcp's adapters use
  `--dangerously-skip-permissions` / bypass-sandbox because it exists
  for delegation; this skill's review mode never copies those flags.
  Permission/approval modes ("plan") are politeness-class — grok's
  plan mode auto-approved a real file write (verified 2026-07-14) —
  so rows relying on them are review-eligible only after a
  write-attempt probe passes. Currently OS-verified: codex
  (`-s read-only`), grok (`--sandbox read-only`). A reviewer that can
  write is a defect ([DOM-11]: the reviewer must not implement).
- **The skill owns invocation mechanics; review-loops owns policy.**
  No policy restatement in the skill; no flags in the runbook.
- **Flag tables carry verification status.** Each agent row records
  how it was verified (live run vs `--help` inspection) and when.
  Unverified guesses are marked, never presented as known.
- **No new dependencies.** The skill drives already-installed CLIs; if
  a CLI is absent, the skill reports it and falls back per
  review-loops §2 (same-family separate role, then disclosed
  fresh-eyes). It never installs anything.
- **Probe results update the [DOM-13] inventory** in the same session —
  a probe that is run but not recorded is evidence discarded.
- agent-mcp itself is not deprecated, modified, or wrapped; it remains
  fine for delegation use where attached.
- **The skill maintains itself through diagnosis, not workarounds.**
  Maintenance events (including exit-0-bad-completion, empty bodies,
  and write-during-review) route through the skill's step 7 — cheap
  path in-session for self-evident drift, debugging subagent for
  mysteries — and end in a proposed fix to the user; never a silent
  hand-patch, never a silently decaying row.

## 4a. Deviation Log

| Spec ref | Planned behavior | Actual behavior | Rationale | Spec proposal |
|----------|------------------|-----------------|-----------|---------------|

## 4b. Spec Baseline

- `4d98a63` — [DOM-11], [DOM-13], [DOM-15] at plan authoring time
  (clean tree).

## 4c. Proposed Spec Delta

None. Rationale: [DOM-11] already defines independent review (inputs,
no-implement rule, disposition loop) and [DOM-13] already defines the
availability inventory and refresh duty; this skill adds invocation
mechanics that no spec section governs or should govern (flags churn
faster than specs). Promotion strategy: N/A. Challenged at review:
grok (2026-07-14) judged the declaration substantively right (finding
in §7); the effective-class-5 shape is satisfied by this named empty
delta.

## 5. Tasks

1. This plan + `skills/call-agent/SKILL.md` (Draft status) +
   status-index row. Done: files exist, skill follows the template
   section order.
2. Pre-landing independent review (+P: different family). Natural
   choice: an agent this skill documents, invoked *by the skill's own
   documented command* — the review doubles as a live validation of at
   least one row. Stance: could you be invoked correctly from this
   skill alone? Is the read-only posture airtight? Is any part
   performative? Is "spec delta: none" right? Is the step-7
   self-maintenance loop (debugging subagent → proposed fix) sound, or
   does it over- or under-trigger? Blocker for task 3.
3. Promotion: flip skill status to Active; add the review-loops §1
   pointer line and crosswalk row; add to COPIED_FILES + repo-map
   renderer; refresh `docs/implementation/03-agent-inventory.md` by
   running the probe procedure against the usable agents (six as of
   2026-07-14: claude, codex, qwen, kimi, grok, opencode) and recording
   verified/blocked per [DOM-13], including gemini's deprecated status.
4. Record promotion baseline; rerun gates.

## 6. Testing Plan — exact commands

- Skill-shape: section order matches `skills/_template/SKILL.md` (by
  inspection).
- Flag-table spot check (no model calls):
  `claude --help | grep -c "permission-mode"` → ≥1;
  `gemini --help 2>&1 | grep -c "approval-mode"` → ≥1;
  `codex exec --help | grep -c "read-only"` → ≥1.
- Live probes (task 3, per skill step 6): liveness ("Reply with
  exactly: PROBE-OK", 120s timeout) plus the write-attempt probe on
  every non-OS-sandbox row; failures and revocations recorded in the
  inventory, not hidden.
- `/Users/van/Developer/backstitch/.venv/bin/backstitch check
  --repo-root .` → 15 spec sections, 0 errors, 0 warnings.
- After task 3: scaffold dry-run output contains
  `skills/call-agent/SKILL.md`.

## 7. Independent Review Loop

Round 1 executed 2026-07-14: grok 0.2.101, invoked via the skill's own
(corrected) documented command — `--sandbox read-only --always-approve`,
`stopReason: EndTurn`, read-only verified by `git status`. The
invocation itself was a live validation arc: the draft row failed
(wrong output-format value → fixed inline, step-7 cheap path), then
produced empty output (→ step-7 deep path: debugging subagent found
plan-mode cancels headless on shell prompts AND auto-approves writes —
a safety finding). Verdict on the revised draft: BLOCKED, F1–F3 P1 +
F4–F7 P2.

| # | Finding (abbrev.) | Disposition |
|---|---|---|
| F1 (P1) | claude/qwen marked verified from `--help` while the skill's own principle demands write-attempt probes for permission-mode rows | **Accepted.** Both demoted to "verify at probe (write attempt)", explicitly not review-preferred until it passes |
| F2 (P1) | Probe write-checks covered only the rows that already had sandboxes — inverted vs risk | **Accepted.** Step 6 now runs a liveness probe plus an explicit write-attempt probe on every non-OS-sandbox row; a successful write revokes review eligibility |
| F3 (P1) | Plan §4 invariant still asserted plan/approval modes as the read-only posture | **Accepted.** Invariant rewritten: only OS-enforced sandboxes count as verified containment; permission modes are politeness-class |
| F4 (P2) | "kimi has no visible read-only mode" is false — `--plan` exists | **Accepted.** Row corrected; `--plan` documented as defense-in-depth, not proof |
| F5 (P2) | Step 7 over-mandates the subagent for trivial drift; under-covers exit-0-bad-stopReason, empty body, write-during-review | **Accepted.** Split into cheap path (self-evident causes, main session) and deep path (mysteries and containment failures, subagent); the three silent failure modes are now first-class triggers |
| F6 (P2) | grok caveats incomplete (macOS network no-op; sandbox fail-open) | **Accepted.** Row now states child-network blocking is Linux-only and a sandbox warning is an invocation failure |
| F7 (P2) | Stale plan §8; resume flags bloat the safety table; formal empty spec delta preferred | **Accepted.** §8 updated; continuity flags moved to a footnote; §4c added as a named empty delta with rationale |

Round 2 (scoped to F1–F7 fixes) below; must PASS before task 3.

## 8. Assumptions and Open Questions

- Gemini CLI is discontinued upstream (Google); the replacement
  antigravity CLI is not yet installed. The skill carries a deprecated
  row and a placeholder; the placeholder becomes a verified row (with
  read-only flag research) when antigravity is installed. Owner: user
  installs; the probe procedure verifies. Reopens on install.
- grok: resolved live 2026-07-14 (a step-7 debugging session found
  `--sandbox read-only --always-approve` OS-enforced, and that
  `--permission-mode plan` is unsafe). claude, qwen, kimi, and
  opencode remain review-eligible-pending: their write-attempt probes
  run at task 3. Reopens if any probe shows a write succeeding.
- Whether sibling repos want per-repo default-reviewer preferences
  (mm uses codex heavily) is deferred to propagation.

## 9. Out of Scope

- Delegation mode (write-enabled invocation) — one note in the skill
  points delegates at agent-mcp or the harness's native subagents;
  this skill is for review.
- Deprecating or modifying agent-mcp.
- Wiring the probe into CI or the coalescing triggers.
