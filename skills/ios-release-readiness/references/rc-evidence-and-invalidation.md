# Final Candidate Evidence and Invalidation

Keep evidence light, locatable, and bound to one exact Candidate. Do not create a second project-management system.

## Final Candidate Identity

Record at least:

```text
App version / build:
Git Source Identity: repository, branch/detached state, full commit, relevant dirty state
Bundle ID:
Target / scheme / Release Configuration:
Platform / SDK / destination identity (`iphoneos` or `iphonesimulator`):
Dependency baseline:
Intended App target `iphoneos` Release build product or existing Archive identity:
Support scope and verified environments:
Testing evidence and physical-device/human boundary:
Trusted Engineering Baseline and Remaining Engineering Risk:
Release-specific verification evidence:
Remaining / nonblocking Deferred evidence:
```

An existing Archive may be identified, inspected, and bound to the Candidate. If none exists, bind final package/build evidence to an identifiable intended App target + Release Configuration product built for an iOS device destination/`iphoneos` SDK, such as a generic iOS device build. Explicitly leave submission Archive creation, final distribution-signing operations, and Archive/Validate checks to Submission Operations.

A Simulator Release product may support Release-mode smoke, Simulator behavior verification, and part of Release-versus-Debug comparison. It cannot alone satisfy the actual build/package evidence required for Ready. If the environment cannot form the required `iphoneos` product and no existing Archive is available, status is Blocked; name that product as the minimum missing technical evidence.

## Reproducible Source Baseline

A dirty working tree is acceptable during investigation when its state and relevant diff are recorded. Do not freeze it as the Final Candidate while release-affecting local state is unknown or irreproducible.

Before Ready:

- give every release-affecting source/configuration change an explicit Source Identity;
- ensure the final product source and configuration can be restored from a clear local Git baseline;
- exclude unknown or unrecorded release-affecting staged, unstaged, generated, or untracked changes;
- identify unrelated user files/docs/untracked material and establish that they do not enter or affect the Candidate.

When repository rules permit, the task is authorized, scope is clear, and unrelated changes are excluded, create a safe local commit if needed for recoverability. Never push, force-push, mutate remote branches/tags, merge, publish, or absorb unrelated work.

## Evidence Sources and Levels

Prefer current upstream evidence instead of rebuilding it:

- Testing Campaign or Final Broad Testing handoff;
- Delta Testing, Fix Verification, and regression evidence;
- user real-device evidence;
- Trusted Engineering Baseline, Source Identity, and Remaining Engineering Risk;
- release build, product/package inspection, and targeted Release smoke evidence.

Label the proven level exactly:

- Simulator Release behavior verified;
- `iphoneos` Release product inspected;
- physical-device install verified;
- physical-device launch verified;
- physical-device behavior verified;
- human physical-device UX verified;
- Deferred / Missing.

Installing or launching does not prove behavior or UX. Reuse credible physical-device evidence only when the Candidate has not changed the behavior it proves.

## Fresh Install Applicability

Require Fresh Install or equivalent clean-state evidence when first-run state, permission prompts, migration, caches, persistence, Keychain/container state, cold start, or prior-version data can change the result. If none apply, record why and use the lightest sufficient clean-state check.

## Change Impact and Evidence Invalidation

Whenever behavior, configuration, dependency, entitlement, capability, resource, or package content changes:

1. identify the exact change and direct/indirect impact surface;
2. mark only affected evidence stale;
3. decide whether Product Confidence, Engineering Confidence, Release Confidence, or more than one changed;
4. route behavior impact to `testing` Delta Testing / Fix Verification;
5. route baseline impact to `code-review` Change Review;
6. rebuild/reinspect the Release product when contents or behavior may change;
7. rerun targeted proof, adjacent regression, and a proportionate core-value Release smoke;
8. form the next Candidate revision and bind only evidence that matches it.

Do not clear everything mechanically. Do not carry old evidence forward silently. Ordinary development commits need no elaborate Candidate lineage.

Typical impact mapping:

- copy/layout → affected layout, localization, accessibility, and supported-size evidence;
- media/export → output correctness, media properties, save/export, and affected main-path evidence;
- permission/entitlement → Fresh Install, prompts, allow/deny/recovery, Settings, declarations, and affected-flow evidence;
- dependency/build setting/resource → rebuild, package composition, affected runtime, and smoke evidence;
- endpoint/flag/logging → Release-only behavior, failure/recovery, data/privacy, and package evidence;
- data model → existing/fresh data, migration, interruption, persistence, recovery, and corruption evidence.

## Final Binding Rule

Freeze the Final Candidate only when:

- Candidate identity is complete and reproducible;
- an existing Archive or an intended App target + Release Configuration `iphoneos` Release product supplies actual build/package evidence;
- the Trusted Engineering Baseline matches the final source or has been updated through Change Review;
- required Testing and user/device evidence remains current for affected behavior;
- release-specific build, product/package/configuration, privacy/dependency/sensitive-data, asset, and smoke checks pass;
- all required technical evidence exists at the level needed to enter Submission Operations;
- remaining evidence is explicitly nonblocking and does not invalidate release trust.

An unavailable agent/device capability does not turn required technical evidence into a valid deferral. Complete agent-operable checks, then request the smallest human action or remain Blocked.

## Deferred Risk

Defer only when the remaining item is clearly nonblocking, does not make the Candidate technically untrustworthy, does not prevent Submission Operations, and is recorded with its evidence boundary and next owner. A low-risk future experience improvement may qualify.

Do not defer a crash, wrong output, data corruption, privacy/security issue, invalid package/configuration, invalid Trusted Engineering Baseline, required technical evidence, or required submission asset. Ask: **Does this unresolved item invalidate release trust in this Candidate?** If yes, the status is Blocked regardless of severity.
