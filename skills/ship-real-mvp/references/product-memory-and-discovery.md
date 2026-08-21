# Product Memory and Discovery

Use this reference when the product problem, scope, or current truth is not yet clear enough to build or change safely.

## Start With the Real Situation

Clarify, in ordinary language:

- who is experiencing what problem and in which situation;
- what they do today and where it breaks down;
- what core action should produce what useful result;
- which constraints, permissions, platforms, or real-world conditions matter.

Do not turn an unstated assumption into a permanent product decision.

## Choose Proportionate Discovery

- **Light:** problem, user, main action, decisive constraints, and a few acceptance checks.
- **Medium:** Light plus scope alternatives, non-goals, meaningful states, risks, and reference intent.
- **Deep:** Medium plus dependencies, tradeoffs, repeated-use scenarios, recovery, and a concise brief confirmation.

Use only the depth that reduces meaningful ambiguity. Continuing an existing product or fixing an unambiguous Bug usually needs less discovery.

## Define the Core Value Loop

Describe the shortest credible path from the user's situation to the desired result. Include a capability only when it is necessary for that path, materially protects its success, or is required by platform, privacy, data, or safety reality.

Keep Later, rejected ideas, and open questions visible. Scope is not a promise to build everything that is imaginable.

## Minimal Product Memory Contract

Create or maintain a compact `PRODUCT.md` when it helps a future collaborator recover product truth:

```markdown
# [Product] — Product

## Problem and User
## Core Value Loop
## Current Scope
## Core Flow
## Non-goals
## Important Defaults and States
## Known Limitations / Deferred Evidence
## Material Product Decisions
```

The file should make the user, situation, value, current boundaries, important states, and accepted limitations recoverable. It is not a full PRD, market study, roadmap, KPI plan, persona taxonomy, Bug archive, or mandatory diagram.

## Confirmation and Updates

When a product choice would change capability, scope, default behavior, user experience, privacy, data behavior, support range, or delivery cost, state the current understanding plainly and ask for the smallest needed confirmation.

Update `PRODUCT.md` when product behavior, flow, scope, defaults, support, important states, or accepted limitations materially change. Do not edit it mechanically for a local fix that restores already-documented behavior.
