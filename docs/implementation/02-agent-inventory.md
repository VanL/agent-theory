# Agent Inventory

## Purpose and Scope

This document records which agent families are currently available in the
environment and which ones are preferred for independent review work.

Keep it lightweight and refresh it when tooling changes materially.

## Governing Spec References

- `docs/specs/00-development-documentation-operating-model.md` [DOM-3]
- `docs/specs/00-development-documentation-operating-model.md` [DOM-11]
- `docs/specs/00-development-documentation-operating-model.md` [DOM-13]

## Verification Method

To refresh this inventory:

1. run a small read-only review or no-op prompt against each available agent
   interface
2. record whether it is:
   - verified usable
   - present but blocked by credentials or configuration
   - present but currently failing at invocation time
3. update the refresh date and notes

## Current Observed Availability

Last refreshed: 2026-04-07

| Agent family | Status | Notes |
|--------------|--------|-------|
| Claude | verified usable | Claude Code review succeeded after retrying with a narrower prompt |
| Codex | verified usable | current environment is running on Codex tooling |
| Gemini | present but blocked | Gemini tooling is present but review failed due to missing `GEMINI_API_KEY` |
| Qwen | present but failing | Qwen tooling is present but the current wrapper failed during invocation |
| Kimi | not observed | no Kimi interface is currently recorded in this environment |

## Review Preference

For plan review and final review:

1. prefer a different agent family than the authoring agent
2. if several are available, prefer one that has not already shaped the plan
3. if only one family is available, note that limitation and do a stricter
   fresh-eyes review

## Refresh Guidance

Update this file when:

- the available tool surface changes
- a new agent family becomes available
- an existing agent family is removed
- review workflow preferences change materially

## Related Plans

- `docs/plans/2026-04-07-review-skills-bootstrap-plan.md`
