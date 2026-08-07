# Specs Index

This directory holds durable specification surfaces: behavioral contracts
(intended behavior, invariants, verification) and, where useful, **definitional
reference** docs that fix the meaning of framework terms without creating
product obligations.

Use this numbered index as the canonical starting point for specs. Keep
`README.md` as a thin pointer so directory browsing and numbered read order
stay aligned instead of competing.

## Rules

- Behavioral specs define intended behavior, invariants, and verification
  expectations.
- Definitional reference specs (Status: Reference) explain terms and roles;
  they do not override winning product contracts or replace program theory.
- Specs use stable reference codes so plans and code can cite exact
  requirements.
- Specs backlink related plans under `## Related Plans`.
- If behavior changes materially, update the governing behavioral spec before
  or with the code.

## Recommended Starting Points

1. `../program-theory.md` — conceptual identity of **this repository**
   (frames interpretation and placement; not a behavioral contract)
2. `02-agent-theory-and-program-theory.md` — reference primer: what Agent
   Theory and program theory *are* (not session-start mandatory; not product
   theory)
3. `01-development-documentation-operating-model.md` — normative process

## Naming

- Use stable filenames.
- Numbered prefixes are recommended when the corpus is expected to grow.
- Prefer concise, descriptive titles over ticket-like names.

## Related Surfaces

- `docs/plans/` for execution
- `docs/implementation/` for rationale and repository maps
- `skills/` for reusable workflow instructions
