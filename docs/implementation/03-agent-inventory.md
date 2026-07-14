# Agent Inventory

## Purpose and Scope

This document records which agent families are currently available in
the environment and which are preferred for independent review work.
Probe and invocation mechanics are owned by
`skills/call-agent/SKILL.md`; this file holds the observed results.

## Governing Spec References

- `docs/specs/01-development-documentation-operating-model.md` [DOM-3]
- `docs/specs/01-development-documentation-operating-model.md` [DOM-11]
- `docs/specs/01-development-documentation-operating-model.md` [DOM-13]

## Current Observed Availability

Last refreshed: 2026-07-14 (call-agent step-6 probe sweep: liveness +
write-attempt containment)

| Agent family | Status | Notes |
|--------------|--------|-------|
| claude | verified usable, review-eligible | Liveness + write-attempt passed (plan mode diverted the write outside the repo, repo untouched). Usually the authoring agent — prefer others for review of its own work |
| codex | verified usable, review-eligible | OS sandbox (`-s read-only`); six live review rounds 2026-07-14. Known-bad versions: 0.120.0–0.120.2 |
| grok | verified usable, review-eligible | OS sandbox (`--sandbox read-only`), write-block verified by a debugging session; two live review rounds 2026-07-14. Never use its plan mode as containment — it auto-approves writes |
| qwen | present but blocked | API 404 at probe: default model now requires a paid slug (`z-ai/glm-4.5-air`). Re-probe after config/billing change |
| kimi | present, probe incomplete | `--plan` is incompatible with `-p` (headless has no containment mode); write-attempt under plain `-p` pending before review eligibility |
| opencode | present, review eligibility REVOKED | Write-attempt probe succeeded — `opencode run` created a file in the repo despite the brief boundary. Re-probe only after a containment flag or config is found |
| gemini | deprecated upstream | Google discontinued the CLI (2026-07-14); the local binary still answers. Do not use for new reviews |
| antigravity | not installed | Google's gemini replacement; add on install, with containment research |

## Review Preference

1. Prefer a different agent family than the authoring agent, selected
   from the review-eligible rows only — currently codex and grok
   (claude when it is not the author).
2. If several are available, prefer one that has not already shaped
   the plan.
3. If none is available, note the limitation and do a stricter
   fresh-eyes review per `review-loops-and-agent-bootstrap.md`.

## Refresh Guidance

Refresh via the probe procedure in `skills/call-agent/SKILL.md` step 6
when tooling changes materially, a probe-affecting version lands, or an
invocation surprises. A probe run but not recorded here is evidence
discarded.

## Related Plans

- `docs/plans/2026-04-07-review-skills-bootstrap-plan.md`
- `docs/plans/2026-07-14-call-agent-skill-plan.md`
