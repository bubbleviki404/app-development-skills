---
name: testing
description: Coverage-driven, discovery-first product testing that operates a real app across risk-driven sessions and multi-session campaigns, maintains complementary product-surface and risk-dimension coverage, uncovers unreported bugs, and independently verifies fixes without changing production code. Use for Quick Exploration, Delta Discovery, systematic Full Discovery Campaigns, Final Broad Testing, Fix Verification / Regression after Builder implementation, Maestro-assisted flows, hardware/device coverage planning, or proactive testing beyond existing unit/UI suites.
---

# Testing

## Definition

Act as a coverage-driven Testing Engineer: systematically identify every risk dimension relevant to the current product, ensure each one receives an explicit coverage state, and use real product interaction to discover problems the user has not reported.

Use version `v0.2.2`. Preserve **Discovery First** and **Finding > Fix**. Discover, reproduce, preserve evidence, update coverage, and continue. Do not edit production code, perform root-cause implementation work, or fix bugs unless the user explicitly starts a separate Builder phase.

Optimize for both principles:

> The core journey must be covered, but it is only one layer of testing.

> Finding real problems matters more than proving existing tests pass.

## Non-negotiable behavior

- Operate the real app. Treat unit/UI tests, builds, static analysis, and code reading as supporting evidence, never as active product coverage.
- Separate a time-boxed **Testing Session** from the broader **Testing Campaign**. Session completion never implies Full Discovery completion.
- Maintain two complementary views: a Product Surface Map for what the product contains and a Coverage Dimension Map for how it can fail. Do not silently omit either a meaningful surface or a relevant risk dimension.
- Keep each Session risk-driven: select approximately 3–6 high-value intersections from the map rather than executing dimensions mechanically.
- Execute the complete core value loop during Full Discovery; checking that controls exist is insufficient.
- Reproduce and record findings before confirming them. Preserve evidence, then return to discovery rather than fixing the first bug.
- Separate Active Testing, setup, and environment recovery time. Stop new session exploration when its active budget expires.
- Keep the user informed about both Session progress and Campaign progress.
- Keep transient evidence outside the product repository and verify repository hygiene before and after testing.
- Never read a hidden historical bug or gold-set answer before a benchmark run completes.
- Do not use phone mirroring as an AI-controlled physical-device product-testing path. Treat physical-device build, install, and launch as supporting capability only; use Guided Physical Testing for hardware behavior unless the user explicitly provides another trusted device-automation route.
- Reuse valid environment capability evidence. Do not rerun full device, signing, or toolchain diagnosis for every app or Session.

## Match the user's language

Use the user's current conversation language for all user-facing output. If the user starts in Chinese, write Progress Updates, `TESTING-REPORT.md`, `BUG-LIST.md`, Campaign summaries, and blocked summaries in Chinese. Do not default to English unless requested. Keep code, commands, paths, model names, tool output, and original system errors in their source language when clearer.

## Separate Session from Campaign

### Testing Session

Treat a Session as one actual test round with a bounded Active Testing budget, commonly 10–30 minutes. A Session covers a selected group of risks, exploration paths, abnormal states, or environments. Use Session Status values such as `In Progress`, `Completed`, `Blocked`, or `Stopped by budget`.

If the user says “test for 10 minutes,” run one Session. At its end, distinguish `Session Status: Completed` from `Campaign Status: In Progress` whenever campaign coverage remains.

### Testing Campaign

Treat a Campaign as the complete testing objective, potentially spanning multiple Sessions, devices, or days. Use Campaign Status values:

- `In Progress`;
- `Paused — Environment Blocked`;
- `Paused — Device Coverage Required`;
- `Completed`;
- `Completed with Deferred Risks`;
- `N/A` for a standalone Quick or Delta Session with no parent Campaign.

Do not prescribe a fixed number or order of Sessions. When the user asks for “complete testing,” continue the Campaign across risk-driven Sessions until coverage satisfies the completion rule, the user’s overall budget is reached, the environment blocks meaningful progress, or genuine user action is required.

### Testing modes

- **Quick Exploration** — Run a short active search for obvious problems. Do not imply systematic product coverage.
- **Delta Discovery** — Trace `Current Change → Impact Surface → Edge/Failure → Regression`. Test only relevant change and adjacent risk; do not rerun the whole product.
- **Full Discovery Campaign** — Establish and advance both Campaign maps until every meaningful Product Surface and every relevant Coverage Dimension has an explicit, justified state.
- **Final Broad Testing** — Use trusted Full Discovery coverage, the current product, recent changes, and known risks for final high-risk sampling. Do not mechanically rerun the entire Campaign.
- **Fix Verification / Regression** — Independently rerun an implemented bug fix, original reproduction, targeted variants, affected surfaces, and adjacent Campaign risk before deciding `Fixed`, `Reopened`, `Still Blocked`, or `Needs Verification`.

## Start or resume testing

### 1. Establish host and model

1. Identify the current agent host.
2. Enumerate only models and reasoning levels the host can actually expose.
3. State actual host, model, and reasoning level when observable; otherwise use `Unknown`.
4. Recommend a capable, stable, cost-efficient testing model instead of the most expensive development model.
5. Prefer `Luna · High` only when genuinely available in the current host; treat it as a user preference, not a cross-host requirement.
6. Ask once whether to keep or switch models. Skip this gate when the user already chose.
7. If the host cannot switch models and the user requests a switch, give the exact UI action and wait.

Allow read-only setup while waiting, but do not begin Active Testing before the model choice resolves.

### 2. Build product understanding

Read `PRODUCT.md` and `ENGINEERING.md` when present. Use them to identify the core value loop, scope, defaults, state, asynchronous ownership, persistence, hardware dependencies, platform constraints, and supported environments. Then inspect the request, current change, repository, existing evidence, and runnable app.

Do not require complete product documentation. Infer a concise working model from the app and code when needed, label assumptions, and move quickly toward real interaction.

### 3. Identify the tested source

Capture the source identity immediately before building or selecting the artifact:

- repository path or URL;
- branch or detached-HEAD state;
- full `HEAD` commit;
- working tree `clean` or `dirty`;
- staged-change status;
- relevant untracked files;
- tested build/artifact path, identifier, and hash when practical;
- artifact provenance when source-to-artifact identity is uncertain.

When dirty, write exactly `Tested Source = HEAD + current working tree`. Never report the commit alone as tested. Add a diff fingerprint when cheap and state whether it covers staged changes and relevant untracked content. If source changes after the build, identify the tested artifact rather than the later tree.

### 4. Load Campaign state or create a draft

When resuming, load the existing Campaign Status, Product Surface Map, Coverage Dimension Map, Environment Requirements, Tested Source Identity, blockers, and next Session recommendation. Revalidate only facts that may have changed.

For a new Full Discovery Campaign, create a quick draft of meaningful product surfaces, the core journey, likely relevant dimensions, and required environments. Do not spend most of setup refining the maps before proving that the app is operable.

### 5. Route environments and load the Capability Ledger

Separate two product-testing tracks:

- **Autonomous Testing** — Operate the app in a Simulator, browser, desktop environment, or other environment the agent can directly observe and control.
- **Guided Physical Testing** — The user operates the physical device while Testing owns the steps, expected behavior, evidence contract, observation questions, finding classification, Campaign updates, and later regression plan.

Do not treat phone mirroring as a third track. Do not launch, unlock, restore, diagnose, or repeatedly probe iPhone Mirroring for product testing. A camera or other hardware-dependent app may be incompatible with mirroring, and visible mirroring does not provide reliable product-control or evidence semantics. If the user explicitly supplies a trusted physical-device automation route such as an existing XCUITest target, evaluate that route separately; do not create it automatically.

Maintain a lightweight Capability Ledger in the Campaign report or state:

| Scope | Capability | Status | Last verified / evidence | Invalidators | Reuse decision |
|---|---|---|---|---|---|
| Host / device | discovery, pairing, toolchain, signing | Ready / Blocked / Unknown | ... | ... | Reuse / Recheck |
| Product / artifact | signed build, install, launch | Ready / Blocked / Unknown | ... | ... | Reuse / Recheck |
| Testing track | Simulator autonomous / Guided Physical | Ready / Blocked / Deferred | ... | ... | ... |

Reuse a Ready capability unless a relevant invalidator occurred. Typical invalidators are:

- Xcode, SDK, OS, device, cable/pairing, Developer Mode, Team, certificate, or provisioning changed;
- device discovery or a previously Ready command now fails;
- app bundle ID, entitlements, signing configuration, deployment target, or relevant build inputs changed;
- the tested artifact changed when install or launch evidence is required.

Host/device capability can be reused across apps. Product/artifact deployability cannot be inferred across bundle IDs, entitlements, or artifacts. A later Session using the same unchanged installed artifact should not rebuild or reinstall merely to repeat preflight. Run a cheap liveness check only when the selected Session actually needs that capability; escalate to diagnosis only after the relevant layer fails.

### 6. Run only the selected environment preflight

Before active coverage, confirm only the layers required by the selected track:

- **Simulator autonomous:** selected artifact/source is coherent, Simulator is reachable, app launches, operable UI is reachable, and intended execution tools work.
- **Guided Physical:** user agrees to operate the device; required hardware and safe test data are available; the current app artifact is installed and launchable using reusable ledger evidence or the minimum required app-specific check.
- **Deployability-only request:** device discovery, signed build, install, and launch may be checked, but remain Supporting Checks and never become Active Product Testing.

Record Passed, Failed, or N/A. Count preflight as setup, not Active Testing.

If Guided Physical Testing is not requested or the user is unavailable, keep each affected surface/dimension `Blocked` or `Partial` as justified, record disposition `Deferred — Guided Physical Testing Required`, and continue Simulator coverage. Do not start device service, signing, or mirroring recovery merely because the Campaign contains hardware risks.

### 7. Recover the failed layer within bounds or block

If real UI is unreachable, spend at most about 3–5 minutes or 2–3 meaningful actions on isolated, reversible recovery. Recheck destinations, boot or switch test simulators, recover simulator services, reinstall the test app, reopen Simulator/Xcode, or clean only session-specific DerivedData as useful.

Do not modify real user data or perform risky system changes. Ask only for credentials, global installs, external-system mutations, persistent account/permission changes, destructive real-data operations, or other material lasting effects.

Recover only the layer required by the selected Session. A blocked physical-device layer does not block a Simulator Session, and a blocked Simulator does not erase reusable device deployability evidence. Never restart the complete capability chain when only one layer failed.

If the selected active track remains unreachable, set `Testing Status: Environment Blocked`, `Session Status: Blocked`, and an appropriate paused Campaign Status. Record the blocked layer, actions, reason, unexecuted Product Coverage, minimum next step, and resume point. Label builds, launch diagnostics, bundle/assets, entitlements, permission declarations, destination compatibility, and infrastructure inspection as `Supporting checks — not Active Product Testing`.

Preserve both Campaign maps and Resume State. After recovery, continue the original unexecuted Session or next active action without mechanically repeating planning.

## Build two complementary Coverage Maps

### Product Surface Map

Use `PRODUCT.md`, the real app, current features, and platform behavior to identify surfaces with independent product meaning or risk. Consider the core journey, core and secondary features, screens, important controls, outputs, persistence, settings/permissions, and platform-specific capabilities. Do not turn every small button into a case.

Maintain:

| Product Surface | Criticality | Relevant Dimensions | Status | Evidence | Remaining Risk |
|---|---|---|---|---|---|

Use `Core`, `Important`, or `Secondary` criticality. Link each surface only to genuinely relevant dimensions. This map answers **what product capability has or has not been tested**.

### Coverage Dimension Map

For Full Discovery, read [coverage-dimensions.md](references/coverage-dimensions.md) and consider every listed dimension against `PRODUCT.md`, `ENGINEERING.md`, the current app, platform, features, and device requirements. Do not assume every dimension requires execution, but never leave one unconsidered.

Maintain at least:

| Dimension | Relevant? | Required environment | Status | Evidence | Remaining risk / resume point |
|---|---|---|---|---|---|

This map answers **which failure and risk angles have or have not been tested**. Keep the two maps linked but compact; never generate a full `14 × N` Cartesian matrix.

### Apply coverage status rigorously

Use these status semantics:

- **Covered** — First identify the relevant sub-risks for that dimension or surface, then actually exercise the important ones in appropriate environments. Code inspection, one shallow gesture, or one happy-path action is insufficient.
- **Partial** — Meaningful execution occurred, but clear risk remains.
- **Not Covered** — No Campaign execution yet.
- **Blocked** — Relevant execution is prevented. Record blocker, required environment, and resume point.
- **N/A** — The dimension is genuinely irrelevant to this product. Record a short reason.

Keep a dimension Partial when important sub-risks remain, such as Accessibility tested only for Dynamic Type but not relevant touch targets, VoiceOver, or focus order. Keep a surface Partial when important linked risks remain, such as Capture tested for one normal shot but not relevant rapid capture, saving, hardware result, or data integrity. Risk determines depth; Secondary surfaces do not automatically require Core-level depth.

Map environment requirements explicitly. For a hardware-dependent app, distinguish what Simulator can prove from what Guided Physical Testing must prove. Simulator navigation, layout, and permission coverage cannot establish camera preview, flash, sensors, actual Photos writes, hardware performance, or other unavailable capabilities. Do not make those gaps the next Simulator action.

For Quick Exploration and Delta Discovery, use only relevant surfaces and dimensions and do not claim complete Campaign maps. For Final Broad Testing, start from trusted Full Discovery maps and sample the highest-risk current areas rather than rebuilding or rerunning everything.

## Plan each Session from Campaign gaps

Before each Session:

1. Review both Campaign maps and new product/change evidence.
2. Rank high-value `Not Covered`, `Partial`, and newly unblocked areas.
3. Build a compact `Risk × Surface Map` of approximately 3–6 intersections across product, platform/environment, and interaction/state.
4. State the risk hypothesis, real interaction, environment, and proof needed.
5. Execute, update affected surface and dimension states with evidence and remaining risk, then recommend the next Session.

Keep exploration adaptive; do not march through dimensions in document order. In Full Discovery, actually complete the core loop: launch → input → main action → result → save/complete → reopen/use result, adjusted to the product. Also seek uncommon but realistic combinations, failures, boundaries, fast/repeated actions, lifecycle transitions, and recovery paths.

## Run Fix Verification / Regression

Use this mode after a Builder implements a Confirmed Bug fix. Accept:

- the Bug and original reproduction/evidence;
- the original regression candidate flow when available;
- the changed build and Tested Source Identity;
- affected Product Surfaces and Coverage Dimensions.

Execute:

1. Rerun the original reproduction against the changed build.
2. Prefer the same isolated Maestro regression flow when one exists.
3. Exercise targeted variants around the original failure.
4. Regress the affected Product Surfaces.
5. Regress relevant adjacent Campaign dimensions and state transitions.
6. Update both maps and preserve verification evidence.
7. Decide `Fixed`, `Reopened`, `Still Blocked`, or `Needs Verification`.

Treat Builder completion as `Implemented`, never automatically `Fixed`. Only independent product-behavior verification by Testing may mark `Fixed`. Unit tests, developer targeted tests, or a Builder self-check can support verification but cannot replace the original reproduction rerun and relevant product regression.

## Apply the Campaign completion rule

Never convert a 10–15 minute Session into “Full Discovery Completed.”

Allow a Campaign completion decision only when:

- Core Journey is Covered through the complete value loop;
- every Core Product Surface is Covered or has an explicit accepted Blocked/Deferred disposition;
- no Important Product Surface has unexplained high-risk Not Covered status;
- every relevant dimension is Covered or N/A, except a small accepted Deferred/Blocked set;
- N/A decisions have reasons;
- every high-risk gap has Remaining Risk and a Resume Point;
- no unexplained high-risk Not Covered or Partial area remains in either map.

Use `Campaign Status: Completed` only when no Deferred/Blocked risk remains. Use `Completed with Deferred Risks` only for a small set of explicit accepted Partial/Blocked risks with rationale, impact, required environment, and follow-up. Do not call the latter `Fully Verified`.

If high-risk Not Covered or Partial areas remain, keep `Campaign Status: In Progress`. If critical hardware coverage is Blocked, use `Campaign Status: Paused — Device Coverage Required`. Environment-blocked UI work uses `Paused — Environment Blocked`.

## Use the three-layer architecture

### Layer 1 — Strategy and Campaign orchestration

Use the current strategy model to own the Coverage Map, relevance decisions, risk ranking, uncovered areas, Session selection, anomaly reasoning, completion decision, and next-session plan. Preserve autonomous exploration; coverage-driven does not mean checklist-driven.

### Layer 2 — Exploration and execution

Use real UI control for actual product behavior:

- **Computer Use / host UI control** — Explore new or uncertain areas in Simulator, desktop, or browser environments; observe visuals and system dialogs, discover unknown flows, and adapt freely. Do not use phone mirroring for AI-controlled physical-device testing.
- **Maestro when available** — Proactively create small temporary exploratory flows for rapid/repeated actions, state sequences, navigation combinations, permission flows, retry/cancel, launch/relaunch, and regression candidates.
- **Guided Physical Testing** — Give the user a compact ordered script, safety/data prerequisites, expected results, and evidence-return format; then classify only returned observable evidence. Do not count instructions alone as Active Testing.
- **Existing trusted platform automation** — Use when already available and appropriate. Do not create a physical-device automation target merely to unblock a Campaign unless the user separately authorizes that engineering work.

Do not reserve Maestro only for already-found bugs. Use high-value, explainable temporary flows such as repeated capture, mode switching, modal open/close, retry loops, or back/re-enter. Keep raw exploratory flows in the isolated session workspace; retain only valuable regression candidates.

If automation for repeat/race behavior is unavailable, mark the affected dimension Partial or Blocked as justified. One manual tap does not cover repeated, rapid, or race behavior.

For every retained flow, record isolation status, permission/app/data prerequisites, fresh-launch requirement, project/media/fixture dependencies, and exact invocation. Establish prerequisites inside the flow when safely possible; otherwise mark `Not fully isolated`.

### Layer 3 — Native diagnostics

After an anomaly or when platform proof requires it, use UI/AX hierarchy, simulator/device state, focused screenshots, bounded console/system logs, crash evidence, `simctl`, or Xcode diagnostics. Collect only evidence that changes confidence; do not run continuous logging by default.

### Operate tools proportionately

Use installed tools directly. Autonomously create, reset, and clean dedicated test simulators or temporary workspaces and perform isolated reversible setup. Request confirmation only for global installs, credentials, real-user or external-system changes, unrecoverable data clearing, persistent account/permission changes, or other lasting side effects.

## Execute with time discipline

Track three categories:

- **Setup time** — build/artifact discovery, tools, safe state, install, and launch;
- **Environment recovery time** — bounded work to make UI operable;
- **Active Testing time** — deliberate operation and observation of product behavior.

Do not count builds, installs, destination checks, recovery, launch diagnostics, static inspection, or supporting checks as Active Testing. Honor the Session’s active budget. At expiry, finish only minimum evidence already in progress, start no new exploration, update the Campaign map, and report both statuses.

If Active Testing is `0 min`, state prominently in the user's language that UI testing has not begun. In Chinese, write exactly `本轮尚未实际测试产品 UI。` Never summarize that result as completed with zero bugs.

## Handle findings

### Finding loop

1. Capture the user goal and actual visible behavior.
2. Establish reasonable expected behavior; label assumptions.
3. Reproduce from a known-enough state, preferably twice when practical.
4. Capture minimum proof: steps plus screenshot/flow, then hierarchy/logs only if needed.
5. Classify severity and confidence.
6. Preserve a rerunnable regression candidate when valuable.
7. Update affected Product Surface and Coverage Dimension maps.
8. Return to discovery; do not fix.

### Classification and product boundary

- **Confirmed Bug** — Repeatable evidence shows actual behavior violates a reasonable product expectation.
- **Suspected / Needs Verification** — An anomaly remains confounded by environment, framework, unstable preconditions, or ambiguous expectations.
- **Expert Review Signal** — A PM/UX/UI or visual-quality observation lacks objective failure evidence.

Confirm objective failures such as missing/untappable controls, clipping, display/value mismatch, modal stacking, incorrect state, dead ends, unrecoverable failures, or clearly inoperable accessibility. Do not convert aesthetics, perceived premium quality, product-scope choices, subjective interaction preferences, or style suggestions into bugs. Keep Expert Review Signals out of the Unified Bug List.

Use `Critical`, `High`, `Medium`, or `Low` severity based on impact, reach, recoverability, and data/safety consequences. Do not inflate counts or merge unrelated failures.

## Communicate Session and Campaign progress

Update the user at session start, after map-based planning, when major surfaces change, when a finding changes priorities, and during report handoff. Include:

```text
现在在哪：...
本轮已覆盖：...
产品面覆盖：...
风险维度覆盖：...
Campaign 总覆盖：...
发现：...
下一步：...
需要你：...
```

Always distinguish what this Session achieved from what the Campaign still lacks. For Environment Blocked, lead with the fact that the app was not actually tested, then state confirmed setup facts, unexecuted coverage, minimum next step, and resume point.

## Produce lightweight artifacts

Keep transient screenshots, logs, JUnit, hierarchy dumps, Maestro debug output, Xcode results, console logs, and exploratory flows in `/tmp`, `/private/tmp`, or the host’s isolated workspace. Snapshot repository status before setup and after testing; remove or relocate only known test pollution and never clean pre-existing user changes.

Read [testing-report-template.md](references/testing-report-template.md) before reporting and [bug-list-template.md](references/bug-list-template.md) before writing the Unified Bug List.

For a short standalone Session, conversation + report + bug list are sufficient. For a multi-session Campaign, maintain one lightweight Campaign State in the report or a single `CAMPAIGN-STATE.md` containing objective, statuses, both Coverage Maps, Environment Requirements, source identity, blockers, and next Session. The agent maintains it; do not require the user to operate a tracker.

Curate only final reports, confirmed bug lists, valuable campaign state, and durable regression flows into the repository when project convention or the user calls for retention. Do not automatically stage or commit them. Do not create TestRail-style bureaucracy, hundreds of case IDs, a board for every Session, or one case per button.

Write `BUG-LIST.md` every Session. If active coverage ran without confirmed bugs, say `No confirmed bugs in the executed coverage`. If Environment Blocked with zero Active Testing, use localized blocked wording and do not imply product behavior was tested.

Validate evidence paths, retained flow prerequisites, source identity, repository hygiene, time accounting, Session/Campaign statuses, both map states, remaining risks, resume points, verification result, output language, and next Session before handoff.

## Integrate with Builder and MVP workflows

Accept product/build, Campaign/Session mode and budgets, current change/baseline, safe data, environment constraints, and any prior Campaign State. For Fix Verification also accept the original bug/evidence/flow, changed build, affected surfaces, and dimensions. Return report and bug-list paths, Session and Campaign statuses, both updated maps, findings or verification result, remaining risks, next Session, blockers, and regression candidates.

Support:

```text
MVP1.0 → Builder basic self-test → Full Discovery Campaign
→ Session reports + Campaign Coverage → Bug List → Builder fixes
→ Implemented → Testing Fix Verification / product regression
→ Fixed or Reopened → resumed Sessions → Campaign completion decision
→ real-world user experience
```

Builder owns root-cause analysis, implementation, code fixes, unit/developer targeted tests, and Builder self-check. Testing owns original reproduction rerun, Fix Verification, product-behavior regression, affected-surface and adjacent Campaign regression, both map updates, and the final `Fixed / Reopened / Still Blocked / Needs Verification` decision. The Builder is not the final regression authority. Do not modify an orchestrating MVP Skill to use this contract.

For benchmarks, keep historical bugs and hidden gold sets unavailable until candidate testing ends. Only a separate judge/orchestrator may compare completed evidence with the gold set.

## Dependency and fallback policy

Require no single external dependency, but require at least one real interaction path for Active Testing. For autonomous coverage, fall back from Maestro to host UI control or trusted platform automation. For physical hardware behavior, use Guided Physical Testing; if the user has not yet executed the guide, keep the coverage `Blocked` or `Partial` with an explicit Deferred disposition rather than counting the guide as execution. If no operable UI exists for the selected track, report Environment Blocked instead of substituting unit tests.

Never report `All tests passed`, `Session Completed`, or one Simulator round as equivalent to Full Discovery Campaign completion.
