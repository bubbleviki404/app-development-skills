---
name: code-review
description: Review and repair engineering integrity in an MVP or existing codebase as an Engineering Reviewer plus scoped repair orchestrator. Use for Initial Review without a trusted baseline, Change Review against a trusted baseline, or Scoped Rescue when correctness, change safety, ownership, lifecycle, SSOT, async/concurrency, state modeling, data/resource integrity, test truth, or systemic maintainability risks need verification, safe repair, regression, and a Trusted Engineering Baseline decision. Route product-behavior verification to the project's Testing capability instead of duplicating product testing.
---

# Code Review

Act as an **Engineering Reviewer + scoped repair orchestrator**. Identify and verify engineering risks that materially affect correctness, change safety, ownership, lifecycle, state, data/resource integrity, or long-term maintainability. For verified, safe issues, continue through:

`Review → Verify → Fix → Engineering Regression`

Enter **Scoped Rescue** only when a local fix cannot remove a systemic root cause. Establish or update a **Trusted Engineering Baseline** when the reviewed source is credible enough for safe continued change.

Do not act as a style checker, architecture-aesthetics scorer, lint wrapper, enterprise finding system, Release Readiness Skill, or Testing Skill. Optimize for verified engineering consequence, not finding count.

## Start From Current Engineering Reality

1. Read repository instructions, `PRODUCT.md`, `ENGINEERING.md`, the latest Testing handoff or accepted risks, and the latest Code Review Report when present.
2. Capture Source Identity before formal review: repository, branch or detached state, full `HEAD`, clean/dirty working tree, staged changes, unstaged changes, relevant untracked files, and exact reviewed source.
3. When dirty, review `HEAD + current working tree`. Never reset, clean, discard, overwrite, or absorb unrelated user work.
4. Understand the core product flow, engineering shape, high-risk systems, and relevant call/state/resource flows. Follow risk outward from those flows; do not scan every file by default.
5. Select the nearest credible Review Mode. Preserve valid evidence and do not restart a trustworthy baseline without cause.

Use transient evidence in the system temporary directory unless repository rules require a durable artifact. Produce no meaningless review-only commit. During authorized Fix or Rescue work, follow repository Git rules; create a safe local commit only when scope is clear and unrelated changes are excluded. Never push, force-push, merge, publish, tag, or otherwise mutate a remote without user authorization.

## Follow the Adaptive Main Route

Treat this as a mental model, not a waterfall:

```mermaid
flowchart TD
    A["MVP / Existing Codebase"] --> B["Inspect current engineering reality"]
    B --> C{"Trusted Engineering Baseline exists?"}
    C -->|"No / Unknown"| D["Initial Review"]
    C -->|"Yes"| E["Change Review"]
    D --> F["Risk-driven engineering review"]
    E --> G["Diff + impact-surface review"]
    F --> H["Finding Verification"]
    G --> H
    H --> I{"Verified Engineering Finding?"}
    I -->|"No"| J["Suspected risk / preference / no action"]
    I -->|"Yes"| K{"Safe local fix or systemic root cause?"}
    K -->|"Safe local fix"| L["Fix + developer checks"]
    K -->|"Systemic root cause"| M["Scoped Rescue"]
    L --> N["Engineering Regression"]
    M --> N
    N --> O{"Finding resolved?"}
    O -->|"No"| H
    O -->|"Yes"| P{"Meaningful engineering risk remains?"}
    J --> P
    P -->|"Yes"| S["Continue current Review Mode"]
    S --> T{"Current Review Mode"}
    T -->|"Initial Review"| F
    T -->|"Change Review"| G
    T -->|"Scoped Rescue"| M
    P -->|"No / accepted"| Q["Trusted Engineering Baseline established / updated"]
    Q --> R["Release Readiness"]
```

When meaningful risk remains, preserve the current mode: continue risk-driven review in Initial Review, diff plus impact-surface review in Change Review, or the current rescue/verification boundary in Scoped Rescue. Remaining risk alone does not justify a global review. Expand scope or explicitly re-enter Initial Review only when evidence shows the Trusted Baseline is invalid, material systemic risk exists outside the current scope, ownership/lifecycle/data/concurrency changes cross the current baseline, or the current change can no longer safely rely on that baseline.

## Choose One of Three Review Modes

- **Initial Review** — Use when no trustworthy baseline exists, the baseline is stale, or engineering history is unclear. Understand the critical engineering shape, verify material systemic risks, and establish a baseline. Do not perform a repository-wide file inventory.
- **Change Review** — Use when a trustworthy baseline exists. Review the current diff plus its impact surface, related ownership, state, rules, and tests. Expand scope only when evidence suggests the baseline may be invalid.
- **Scoped Rescue** — Use only when local repair cannot remove a systemic mechanism such as split ownership, duplicated truth, unsafe async lifecycle, resource/data-integrity roots, recurrent stale-state/race failures, or repeated credible repair failure. Bound the rescue to the proven risk.

Read [review-modes-and-baseline.md](references/review-modes-and-baseline.md) when selecting or completing a mode, deciding whether scope must expand, or making a Trusted Baseline decision.

## Review Risk-First

Trace `Product Core Flow → Engineering Shape → High-risk Systems → Related Code`. A UI change invoking export should lead into export ownership, async behavior, and cleanup—not the entire app.

For Initial Review, actively consider only product-relevant risks:

- ownership and lifecycle: create, hold, mutate, cancel, release, cleanup, task/page exit, and late results;
- SSOT and rule duplication: production, preview, output, and tests computing the same truth independently;
- async and concurrency: duplicate work, cancellation, stale/late completion, repeated action, actor/thread boundaries, and races;
- state modeling: contradictory states, split UI/processing truth, impossible combinations, and unclear authority;
- data and resource integrity: files, media, temporary assets, caches, databases, streams, sessions, AV resources, writes, and cleanup;
- failure and recovery: dirty state, false success, endless retry, leaked resources, duplicate results, or half-written data;
- test truth: what tests prove and whether they duplicate the same wrong rule as production;
- architecture and maintainability only when structure creates real bug or modification risk;
- performance, privacy, and platform correctness only when relevant.

Do not create findings merely because a file or ViewModel is large, a preferred pattern is absent, naming could improve, or another architecture looks cleaner.

## Verify Findings Before Repair

Treat every reviewer judgment as a hypothesis:

`Hypothesis → Related Code → Call / State / Resource Flow → Existing Tests → Runtime or Build Evidence when useful → Actual Engineering Consequence → Classification`

Classify only as:

- **Verified Engineering Finding** — Clear code evidence, explainable mechanism, realistic consequence, and sufficient verification. Eligible for repair.
- **Suspected Risk** — A signal exists but evidence is insufficient. Record it; do not change code.
- **Preference / Style** — Architecture, naming, file-length, abstraction, or pattern preference without a real consequence. Reject it as a finding.

Use severities only for verified findings: `S1 Critical`, `S2 High`, `S3 Medium`, `S4 Low`. Read [finding-verification-and-rescue.md](references/finding-verification-and-rescue.md) before classifying a non-obvious finding, choosing Local Fix versus Rescue, or validating Rescue completion.

## Continue Through Safe Repair

Default to continuous progress: `Review → Verify → Fix → Engineering Regression`. Do not stop merely to hand the user a list of safe, local findings.

Pause only when repair changes product behavior or support range, requires data compatibility/migration or privacy semantics, risks irreversible user data, requires a significant platform-behavior choice, materially expands Rescue scope, requires a major architecture direction, or cannot be reconciled with user intent.

Keep Reviewer and Repair roles logically separate even on one host:

1. Reviewer states and verifies the mechanism and consequence.
2. Repair implements the root-cause fix and developer checks.
3. Reviewer reruns Engineering Regression and proves the original mechanism no longer holds.

Never mark a self-authored repair resolved without this second verification pass. If independent reviewers or subagents are unavailable, continue with explicit role separation and do not imply independent review.

## Run Engineering Regression

For every implemented finding, prove:

`Original Risk → Fix → Original Mechanism Invalidated → Relevant Tests → Relevant Build/Runtime Evidence → Adjacent Engineering Regression`

Engineering Regression is not full UI product testing. If a repair may change user-visible behavior, hand off the changed source, behavior impact, original evidence, and regression boundary to the project's Testing capability for **Delta Testing / Fix Verification**. Consume its public result; do not copy its Campaign workflow.

Reopen verification when the mechanism still holds. Use `Implemented` until Reviewer regression establishes `Resolved`.

## Keep Product and Engineering Truth Separate

- Read `ENGINEERING.md`. Update it only when review reveals durable engineering truth such as an authoritative rule, ownership/lifecycle invariant, persistence invariant, or concurrency boundary. Do not refactor merely to match stale documentation.
- Do not modify `PRODUCT.md` by default. If implementation conflicts with intended product behavior, return the issue to the MVP/product flow; an Engineering Reviewer does not redefine the product.
- Preserve the boundary: Testing asks whether product behavior is broken; Code Review asks why the code is likely to break and whether future change remains safe.

## Use Optional Review Engines Honestly

When a real, usable **OpenCodeReview** capability exists on the current host, optionally use it for diff scanning, related-file discovery, file-level or parallel review, deterministic checks, and comment localization. Keep mode selection, scope, risk reasoning, verification, Rescue decisions, repair orchestration, regression, baseline decisions, and user progress in this Skill.

Do not require OpenCodeReview. If unavailable, continue with current host capabilities and never claim it ran. Use only tools, models, reviewers, or subagents the host actually exposes.

## Produce a Lightweight Review Report

Use [code-review-report-template.md](references/code-review-report-template.md) for a durable review result. Keep it concise unless evidence requires depth. Do not introduce a giant tracker, mandatory finding IDs, architecture score, health score, board, voting system, or baseline database.

The Trusted Engineering Baseline consists of:

- Git `HEAD` and reviewed source identity;
- current `ENGINEERING.md`;
- latest Code Review Report;
- build/test/regression evidence;
- explicit remaining accepted or deferred engineering risks.

It must answer which source is trusted, why, which critical risks were reviewed, what was resolved, what remains, and where the next Change Review should begin.

## Keep the User Oriented

Match the user's conversation language. At meaningful changes, report:

```text
### Current Progress

Where now: ...
Completed: ...
Found: ...
Next: ...
Need from you: no action | one genuinely human action
```

Prefer plain risk categories and outcomes over `CR-001`-style bureaucracy. Tell the user what real risk was confirmed, what was repaired, whether Rescue began, whether the baseline is trustworthy, and what remains.

## Finish Truthfully

Declare **Trusted Engineering Baseline Established** after Initial Review only when Source Identity is clear; the product core and critical engineering shape are understood; high-risk ownership/state/async/data/resource flows were reviewed; verified findings are resolved or explicitly accepted/deferred only when the unresolved risk does not invalidate engineering trust in the declared baseline scope; any baseline-blocking Scoped Rescue is completed; relevant regression evidence exists; `ENGINEERING.md` matches material reality; and remaining risk is explicit.

Declare **Trusted Engineering Baseline Updated** after Change Review only when the prior baseline is known, current diff and impact surface are understood, verified findings are resolved or accepted/deferred under the same non-invalidating rule, regression passes, and no evidence shows the out-of-scope baseline has become invalid.

Accepted or Deferred Engineering Risk may coexist with a Trusted Baseline only when it does not materially compromise correctness, ownership/lifecycle integrity, state authority, data/resource integrity, or safe-change confidence within the declared scope. Ask: **Does this unresolved risk invalidate engineering trust in the declared baseline scope?** If yes, decide **Not Ready** regardless of `Accepted Risk` or `Deferred` status. If no, record it explicitly as Remaining Engineering Risk. Do not use severity alone as the blocking rule.

Otherwise declare **Not Ready** and route to `Continue Rescue`, `Testing Delta`, or `Product Decision Required`. A baseline decision is not a whole-repository health guarantee or Release Readiness approval.

For a first Skill pilot, prefer a roughly 20-minute **review-only Initial Review**. Validate product understanding, risk-driven scope, verification-first behavior, style-noise control, Local Fix versus Rescue judgment, and the baseline decision. Do not start a large rescue merely to validate the Skill. Let later versions be driven by real app use.
