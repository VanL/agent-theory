# Interface-Review Skill Promotion

Status: completed — landed 2026-07-15
Class: 3+P — promoting a skill that shapes how future agent-facing
surfaces are reviewed (process-material, hence +P; the [DOM-14]
promotion tier supplies the trigger and evidence machinery, this plan
supplies the [DOM-15] record and the review dispositions). Hardening:
N/A — no risky trigger (one skill file + two registration lines).

## 1. Goal and Trigger

The [DOM-14] promotion threshold (3 distinct citations of one workflow
theme) tripped on 2026-07-15 for "review an agent-facing surface
against `designing-agent-facing-interfaces.md`". Promote the procedure
as `skills/interface-review/SKILL.md`: the runbook keeps the eleven
principles; the skill owns the walk, the evidence bar, and the output
contract (findings table, ratified-judgments row, verdict line,
runbook-feedback line).

## 2. Citations (all SHA-verified)

1. taut `docs/plans/2026-07-14-taut-mcp-extension-plan.md` §16.3
   (committed at taut `4a129e9`; §16.4 working-tree in the authoring
   session, cited without SHA) — two design-review rounds of an MCP
   tool surface.
2. mm `docs/implementation/41-Risk-Assessment-FMEA.md` RiskEvaluationApi
   Response Contract (mm `b6bded5`) — contract recovery with file:line
   evidence and an honest untested-fields list.
3. mm `docs/plans/2026-07-15-external-api-mcp-agent-contract-improvements-plan.md`
   §4/§5/§9 (mm `15faadc`) — annotation-contract walk with per-row
   rationale and owner-discussion fold-in.

## 3. Execution Record

Drafted by a delegated Opus worker from the runbook plus the three
exemplars (fences: no subagents, no git writes, per-SHA verification,
no negative conclusions from doc absence — all held). Registration: the
`## Skills` table in `docs/implementation/02-repository-map.md` (the
de-facto skill registry; `skills-lifecycle.md` prescribes layout, not a
named index) plus a back-pointer in the runbook's Review Use.
Orchestrator review, then a scoped different-family (grok) round.

## 4. Review Dispositions

Grok round (read-only, 2026-07-15; transcript in the session scratchpad
`skill-review-out.json`): **PASS-with-changes**. Exemplar-fidelity
checks all held (ratified-judgments concept, taut response-guidance
locality claim, `action_priority` exemplar, derived-state-read clause —
none confabulated). Findings, all applied before landing:

| ID | Sev | Finding (gist) | Disposition |
|----|-----|----------------|-------------|
| F1 | P2 | The skill's own evidence-bar example cited `risk_api.py:280` — the `action_priority` line, not the `rpn` assignment (`:274`); the skill failed its own file:line bar | Fixed: re-pinned to `:274` (verified) |
| F2 | P3 | Taut locality claim tense implied confirmed reusability; taut still holds the pattern pending | Fixed: present tense, "pending a second surface" |
| F3 | P3 | `action_priority` attribution conflated model field and view write path | Fixed: both named |
| F4 | P3 | Verdict vocabulary mixed gate form with the exemplars' design-lens form | Fixed: exemplar form (`no blocker` / `blocker: F<ids>`) |
| F5 | nit | Principle 11 name truncated | Fixed: full runbook name |
| F6 | nit | Duplicated Review-Use applicability in two workflow steps | Fixed: one sentence, attributed "per the runbook's Review Use" |
| F7 | nit | One bare runbook path | Fixed: full repo-relative path |
| F8 | P3 (process) | Peer material skills landed with dated plans; promotion needed a [DOM-15] record before Active | Fixed: this plan |

## 5. Verification

- Skill present; registry row and runbook back-pointer grep-verified.
- `python3 bin/check-dom15-fixtures` exit 0; backstitch self-corpus
  check 0 errors / 0 warnings.
- Promotion rows (watermark, deferral, run log) applied to
  `docs/coalescing.md` in the same landing.

## 6. Out of Scope

- Propagation to consumer repos (rides the next guidance wave;
  COPIED_FILES scaffolding then). mm's promotion-tier row gets a
  one-line completion note now, since mm's state file tracked the
  candidate at 2/3.
