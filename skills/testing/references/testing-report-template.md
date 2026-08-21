# Testing Report Template

Render every user-facing heading, field label, explanation, and summary in the user's current conversation language. If the session is Chinese, translate the English scaffold and write the report in Chinese. Keep commands, code, model names, paths, and original errors in their source language when clearer.

Use this as a compact per-Session report plus current Campaign snapshot. Record execution, not intention. Preserve all top-level sections, using concise `None` or `N/A` values where appropriate.

## Template sections

- User Summary and Status
- Tested Source Identity
- Capability Ledger and reuse decision
- Environment Requirements and Preflight
- Product Surface Coverage and Campaign Dimension Coverage
- Session Plan and Actual Coverage
- Fix Verification / Regression when applicable
- Findings and Evidence
- Repository Hygiene
- Campaign Decision, Resume State, and Handoff

```markdown
# Testing Report — <Product / Build>

## User Summary

<Say plainly what this Session actually tested and what the Campaign still lacks. Summarize product surfaces separately from risk dimensions. Never say “Full Discovery Completed” merely because one Session ended. If Active Testing is 0 min, lead with that; in Chinese include exactly: 本轮尚未实际测试产品 UI。>

## Session and Campaign Status

| Field | Value |
|---|---|
| Campaign ID / Objective | <identifier and objective, or N/A> |
| Session ID | <identifier> |
| Date | <timestamp and timezone> |
| Host | <Codex / Cursor / other> |
| Actual model | <model or Unknown> |
| Reasoning level | <level or Unknown> |
| Testing mode | <Quick Exploration / Delta Discovery / Full Discovery Campaign / Final Broad Testing / Fix Verification / Regression> |
| Session Status | <In Progress / Completed / Blocked / Stopped by budget> |
| Campaign Status | <In Progress / Paused — Environment Blocked / Paused — Device Coverage Required / Completed / Completed with Deferred Risks / N/A> |
| Execution tools | <Maestro / Computer Use / browser / native tools / other> |
| Active Testing time | <duration> |
| Setup time | <duration> |
| Environment recovery time | <duration> |
| Evidence overrun | <duration or None> |

## Tested Source Identity

| Field | Value |
|---|---|
| Repo | <path or URL> |
| Branch | <branch or detached HEAD> |
| HEAD | <full commit> |
| Working tree | <clean / dirty> |
| Tested Source | <If dirty, write exactly: Tested Source = HEAD + current working tree; otherwise HEAD> |
| Staging status | <clean / staged paths summary> |
| Relevant untracked files | <paths or None> |
| Diff fingerprint | <digest and covered inputs, or Not recorded> |
| Tested build / artifact | <path, build ID, hash when practical> |
| Artifact provenance | <source-to-artifact evidence, or Unknown> |

## Baseline and Current Change

<Trusted baseline, current change, product assumptions, and Campaign inheritance.>

## Capability Ledger

| Scope | Capability | Status | Last verified / evidence | Invalidators | Reuse decision |
|---|---|---|---|---|---|
| Host / device | <discovery / pairing / toolchain / signing> | <Ready / Blocked / Unknown> | ... | ... | <Reuse / Recheck and reason> |
| Product / artifact | <signed build / install / launch> | <Ready / Blocked / Unknown> | ... | ... | <Reuse / Recheck and reason> |
| Testing track | <Simulator autonomous / Guided Physical> | <Ready / Blocked / Deferred> | ... | ... | ... |

Record only capabilities relevant to this Campaign. Reuse valid prior evidence; do not rerun full device or signing preflight without an invalidator. Do not list phone mirroring as a physical-device testing track.

## Environment Requirements

| Capability / Risk | Required environment | Current environment | Coverage implication |
|---|---|---|---|
| ... | <Simulator / real device / browser / service / fixture> | ... | <Available / Blocked / Partial> |

## Testing Environment Preflight

Selected track: <Simulator autonomous / Guided Physical / Deployability-only supporting check>
Why preflight ran: <new Campaign / relevant invalidator / changed artifact / prior failure / N/A — reused ledger>

| Check | Result | Evidence / Detail |
|---|---|---|
| Build or artifact usable | <Passed / Failed / N/A> | ... |
| Simulator / device reachable | <Passed / Failed / N/A> | ... |
| App installable | <Passed / Failed / N/A> | ... |
| App launchable | <Passed / Failed / N/A> | ... |
| Operable product UI reachable | <Passed / Failed / N/A> | ... |
| Intended testing tools available | <Passed / Failed / N/A> | ... |

For Guided Physical Testing, “operable product UI” means the user can operate the installed app and return the requested evidence. For deployability-only checks, build/install/launch do not establish product UI behavior.

## Environment Recovery / Blocker

- Testing Status: <Environment Blocked / Not blocked>
- Blocked layer: <build / destination / install / launch / operable UI / tool / capability / None>
- Blocker propagation: <selected Session only / Guided Physical only / Campaign-wide, with reason>
- Recovery budget and actions: <limits, actions, results, elapsed time>
- Supporting checks — not Active Product Testing: <checks and evidence, or None>
- Product Coverage not executed: <dimensions/paths or None>
- Minimum next step: <smallest user/environment action or None>
- Resume point: <first unexecuted active action or N/A>

## Product Surface Coverage

| Product Surface | Criticality | Relevant Dimensions | Status | Evidence | Remaining Risk |
|---|---|---|---|---|---|
| ... | <Core / Important / Secondary> | ... | <Covered / Partial / Not Covered / Blocked / N/A> | ... | ... |

List surfaces with independent product meaning or risk, not every small control. A surface is Covered only when its important linked risks were actually exercised; otherwise use Partial.

## Campaign Coverage

| Dimension | Status | Evidence | Remaining Risk |
|---|---|---|---|
| Core Journey | <Covered / Partial / Not Covered / Blocked / N/A> | ... | ... |
| Negative / Failure | ... | ... | ... |
| Boundary | ... | ... | ... |
| State Transition | ... | ... | ... |
| Rapid / Repeated / Abuse | ... | ... | ... |
| Race / Async | ... | ... | ... |
| Lifecycle | ... | ... | ... |
| Persistence / Recovery | ... | ... | ... |
| Device / Adaptation | ... | ... | ... |
| Accessibility | ... | ... | ... |
| Hardware / Platform-specific | ... | ... | ... |
| Stress / Performance | ... | ... | ... |
| Data Integrity | ... | ... | ... |
| Privacy / Destructive Behavior | ... | ... | ... |

For N/A, give a reason in Remaining Risk. For Blocked, include blocker, required environment, and resume point. For Quick/Delta without a Full Campaign, include only the relevant subset and label the map non-exhaustive.

## Session Coverage Strategy

| Priority | Coverage dimension | Product surface | Environment | Interaction/state | Risk hypothesis | Proof needed |
|---|---|---|---|---|---|---|
| 1 | ... | ... | ... | ... | ... | ... |

## Session Actual Coverage

| Area | Actions actually performed | Surface update | Dimension update | Result | Evidence |
|---|---|---|---|---|---|
| ... | ... | <old → new> | <old → new> | ... | ... |

If Environment Blocked before UI interaction, write a localized equivalent of `No Active Product Testing executed.`

## Fix Verification / Regression

- Bug: <ID and original report>
- Builder result: <Implemented build and source identity>
- Original reproduction rerun: <Passed / Failed / Blocked plus evidence>
- Maestro regression flow: <same isolated flow rerun, unavailable, or N/A>
- Targeted variants: <actions and results>
- Affected Product Surface regression: <surfaces and results>
- Adjacent Campaign regression: <dimensions/state transitions and results>
- Verification result: <Fixed / Reopened / Still Blocked / Needs Verification>
- Coverage updates: <surface and dimension changes>

Omit this section when not applicable. Never mark Fixed from unit tests or Builder assertion alone.

## Confirmed Bugs

- `<BUG-ID> — <title>` — <severity>, <confidence>, reproduced <count>/<attempts>. See `BUG-LIST.md` and <evidence>.

If active coverage ran and none were confirmed: `No confirmed bugs in the executed coverage.`

If Active Testing is 0 min: `Not applicable — product UI was not tested.` In Chinese include `本轮尚未实际测试产品 UI。`

## Suspected / Needs Verification

- `<SUSPECT-ID> — <signal>` — <ambiguity and cheapest verification>.

## Expert Review Signals

- `<SIGNAL-ID> — <objective observation>` — <why PM / UX / UI review owns it>.

## Evidence

- `<path or artifact URI>` — <what it proves and retention status>.

## Regression / Exploratory Flows

| Flow | Purpose | Retention | Isolation | Preconditions | Rerun |
|---|---|---|---|---|---|
| ... | <exploration / regression> | <temporary / curated> | <Isolated / Not fully isolated> | <permission, app, data, launch, fixture> | `<exact invocation>` |

## Repository Hygiene

| Check | Result |
|---|---|
| Working tree before setup | <status> |
| Working tree after testing | <status> |
| Testing-created pollution | <None / removed / remaining delta> |
| Durable artifacts copied into repo | <paths and reason, or None> |

## Campaign Decision and Next Session

- Completion assessment: <why Campaign status is justified>
- High-risk Partial / Not Covered: <surfaces and dimensions or None>
- Deferred / Blocked risks: <risk, rationale, required environment, follow-up or None>
- Next highest-value Session: <dimensions, environment, and reason>
- Capability reuse: <what remains valid, what must be rechecked, and the exact invalidator>

## Resume State

- Campaign Status: <status>
- Product Surface Map: <this section or durable state path>
- Coverage Dimension Map: <this section or durable state path>
- Planned but unexecuted coverage: <ordered items>
- Tested Source Identity: <section reference>
- Current blocker: <blocker or None>
- Next active action: <action>

## Handoff

- Builder input: `BUG-LIST.md`
- Campaign state: <path or this report>
- Regression candidates: <paths or None>
- Fix Verification result: <Fixed / Reopened / Still Blocked / Needs Verification / N/A>
- User/environment action: <None or minimum action>
```

Quality checks:

- Match the user's language.
- Show Session Status and Campaign Status separately.
- Never equate Session completion, a time budget, Simulator completion, or zero findings with Full Discovery completion.
- Make setup, recovery, and Active Testing separately auditable.
- For Full Discovery, give every relevant dimension one explicit state and explain N/A/Blocked decisions.
- Keep Product Surface Coverage and Campaign Dimension Coverage complementary; do not generate a Cartesian matrix.
- Ensure Core surfaces and high-risk Important surfaces satisfy the completion rule.
- Require real core-loop execution before Core Journey becomes Covered.
- Identify important sub-risks before marking either a surface or dimension Covered; otherwise use Partial.
- Treat Builder output as Implemented until Testing independently verifies product behavior.
- Keep planned work out of Session Actual Coverage and supporting checks out of Active Testing.
- Distinguish Simulator autonomous evidence, deployability supporting checks, and Guided Physical evidence.
- Reuse valid Capability Ledger evidence and show an invalidator before repeating full preflight.
- Never route physical-device product testing through phone mirroring.
- Preserve remaining risk, resume points, and the next Session.
- Verify evidence links, source identity, flow prerequisites, and repository hygiene.
- Keep subjective PM/UX/UI signals out of Confirmed Bugs.
