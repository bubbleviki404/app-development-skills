# Finding Verification and Scoped Rescue

## Verification Chain

Start every concern as a hypothesis. Establish:

1. **Related code** — exact locations and boundaries involved.
2. **Flow** — call, state, data, resource, ownership, or lifecycle path that makes the concern possible.
3. **Existing tests** — what they prove, omit, or duplicate from production.
4. **Supporting evidence** — targeted build, static diagnostic, test, runtime trace, or reproduction when it changes confidence.
5. **Consequence** — a realistic correctness, integrity, lifecycle, ownership, or safe-change failure.
6. **Classification** — Verified Engineering Finding, Suspected Risk, or Preference/Style.

## Severity

- **S1 — Critical:** credible severe data corruption, security/privacy harm, corruption of core state, or core correctness collapse.
- **S2 — High:** likely user-visible wrong result, race/stale state, lifecycle/ownership failure, or serious modification risk.
- **S3 — Medium:** real engineering consequence with narrower trigger or impact.
- **S4 — Low:** real engineering value but not a current baseline blocker.

Do not assign severity to style preferences.

## Local Fix

Use a Local Fix when the mechanism is verified, intended engineering truth is clear, repair is bounded and reversible, affected behavior is understood, and targeted plus adjacent regression can prove removal. Continue without a user gate when it does not change product meaning, support scope, privacy/data semantics, or major platform behavior.

## Scoped Rescue

Enter Rescue only when local repair would leave the root mechanism intact, particularly for systemic ownership/lifecycle ambiguity, multiple sources of truth, unsafe async cancellation/late results, unclear resource cleanup, data-integrity roots spanning call sites, recurrent races/stale state, repeated credible repair failure, or architecture that demonstrably makes current modification unsafe.

Before changing code, state the verified mechanism and consequence; subsystem in scope and explicit exclusions; authoritative owner/source/invariant after repair; required migration or compatibility choices; regression proof; and stop condition.

Pause for user direction if scope expands materially or requires a product, compatibility, privacy, irreversible-data, support-range, platform-behavior, or major architecture choice.

## Rescue Completion Proof

Require a risk-specific before/after comparison:

| Before | After | Proof |
|---|---|---|
| Three duplicated product-rule implementations | One authoritative production rule used by every call site | Call-site inspection plus tests against production truth |
| Task has no owner and writes late state after exit | Owner/cancellation lifecycle is explicit; late result is ignored safely | Targeted lifecycle evidence plus adjacent regression |
| Multiple partial writers can leave corrupt output | One atomic write boundary and defined recovery | Failure-injection or targeted integrity evidence |

Do not finish Rescue because file organization, abstractions, or naming improved. Finish only when before/after evidence proves risk reduction and adjacent engineering behavior remains credible.

## Engineering Regression Record

For each repair record the original mechanism/evidence, changed locations, root-cause rationale, developer checks, proof the mechanism is invalid, relevant build/test/runtime evidence, adjacent ownership/state/resource regression, user-visible behavior impact, and status: `Implemented`, `Resolved`, `Reopened`, or `Needs Verification`.

Route possible user-visible behavior changes to the project's Testing capability for Delta Testing / Fix Verification. Keep its product-behavior verdict separate from engineering finding status.
