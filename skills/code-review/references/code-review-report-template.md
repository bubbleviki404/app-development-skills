# Code Review Report Template

Keep the report proportional. Omit empty ceremony; retain evidence needed to resume safely.

```markdown
# Code Review Report

## User Summary
- Current engineering trust:
- Confirmed and handled:
- Still worth watching:
- Next route:

## Review Mode
Initial | Change | Rescue

## Source Identity
- Repo:
- Branch / detached:
- HEAD:
- Working Tree: clean | dirty
- Staged:
- Unstaged:
- Relevant Untracked:
- Reviewed Source: HEAD | HEAD + current working tree

## Product / Engineering Understanding
- Core product flow:
- Critical engineering shape:
- Important invariants / ownership:

## Review Scope
- Included:
- Impact paths followed:
- Explicitly excluded:
- Scope rationale:

## Baseline Build / Test Evidence
- Commands or runtime checks:
- Results:
- Evidence limitations:

## Verified Engineering Findings
### Finding title
- Severity: S1 | S2 | S3 | S4
- Location:
- Evidence:
- Root Engineering Mechanism:
- Real Consequence:
- Why Verified:
- Repair:
- Verification:
- Status: Open | Implemented | Resolved | Accepted Risk | Deferred | Needs Verification

## Suspected Risks
- Signal, missing proof, and resume condition. No code change made.

## Explicit Non-findings / Style Preferences Rejected
- Observation and why no engineering consequence was established.

## Repair / Rescue Summary
- Local fixes:
- Rescue scope and exclusions:
- Before/after risk reduction:

## Engineering Regression
- Original mechanisms invalidated:
- Tests / build / runtime evidence:
- Adjacent regression:
- Product-behavior impact requiring Testing Delta:

## ENGINEERING.md Changes
- Durable engineering truth added or corrected:
- Or: No update required; repair was local and existing truth remains accurate.

## Remaining Engineering Risk
- Accepted:
- Deferred:
- Effect on declared baseline scope:
- Does this unresolved risk invalidate engineering trust in the declared baseline scope? Yes | No
- Rationale:
- Resume conditions:

## Trusted Baseline Decision
Established | Updated | Not Ready
- Trusted source and reason:
- Scope of trust:
- Baseline-blocking unresolved risk, if any:
- Decision rule: Accepted/Deferred status does not override a `Yes` trust-invalidation result.
- Next Change Review starting point:

## Next Route
Release Readiness | Continue Rescue | Testing Delta | Product Decision Required
```

Use finding IDs only when volume or cross-session coordination makes them materially useful. Do not add a board, architecture score, health score, multi-reviewer vote, or large baseline database.
