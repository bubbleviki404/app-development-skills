---
name: ios-release-readiness
description: Verify that one exact iOS Release Candidate is technically coherent, release-configured, evidence-backed, and ready to enter App Store Submission Operations. Use after MVP2.0 when a Trusted Engineering Baseline and current Testing/user evidence exist, or when release-specific configuration, package, privacy, dependency, sensitive-data, asset, Release-mode behavior, Final Candidate, evidence binding, or readiness status must be inspected. Route product testing to testing, engineering-baseline review to code-review, and unstable product direction to ship-real-mvp; do not Archive, Validate, upload, submit, or publish.
---

# iOS Release Readiness

Status: **Pilot Ready**. Validate this version through the first complete real-App Release path before calling it Production Proven.

## Definition

Verify that one exact iOS Release Candidate is technically coherent, release-configured, evidence-backed, and ready to enter App Store Submission Operations.

Answer: **Can this exact Release Candidate safely enter submission operations?**

Do not answer whether the whole product is bug-free or desired by users; that is Product Confidence from MVP, Testing, and User Experience. Do not answer whether the whole codebase is trustworthy; that is Engineering Confidence from `code-review` and its Trusted Engineering Baseline. Own Release Confidence: whether the exact build, configuration, package, assets, and still-valid evidence form a trustworthy Final Candidate.

## Entry Contract and Routing

Normally enter with:

- MVP2.0;
- a current Trusted Engineering Baseline, its Source Identity, and Remaining Engineering Risk;
- current Testing Campaign or Final Broad Testing handoff plus relevant regression, user, and physical-device evidence;
- `PRODUCT.md`, `ENGINEERING.md`, current source, release assets, privacy/support information, and any identifiable Release product or existing Archive.

Prefer credible existing evidence. Do not restart Full Discovery, Product Discovery, or Initial Code Review merely to operate this Skill.

Route instead of copying another Skill's work:

- missing, invalid, or materially stale Trusted Engineering Baseline → `code-review`;
- obvious unfinished objective product testing or behavior affected by a Candidate change → `testing`;
- unstable direction, scope, core UX, or unresolved product meaning → `ship-real-mvp`;
- unfinished creative assets → the owning asset/design workflow;
- submission-ready Candidate → Submission Operations.

Consume only the public handoff from each upstream Skill. Do not reproduce its internal state machine, campaign maps, review modes, trackers, or templates.

## Follow the Adaptive Main Flow

Use this as a mental model, not a waterfall:

```text
Trusted Engineering Baseline
→ Inspect current release reality
→ Check upstream evidence freshness
→ Define Release Candidate baseline
→ Release-specific verification
→ Release configuration / package inspection
→ Privacy / dependency / sensitive-data inspection
→ App Store asset readiness
→ Release-mode smoke and invalidated-evidence checks
→ Objective release blocker?
    Yes → Fix or route to owner
        → invalidate affected evidence
        → refresh Testing / Code Review evidence when required
        → rebuild Candidate
        → continue readiness
    No  → Freeze Final Candidate
→ Final evidence binding
→ Ready for Submission Operations / Blocked
```

At the start, inspect repository instructions, branch/HEAD, staged and unstaged changes, relevant untracked files, schemes, targets, build settings, dependencies, existing release products, evidence, approved assets, and support intent. Establish facts from source, configuration, behavior, and the actual product rather than prior prose alone.

Read both references before material release work:

- [iOS readiness checks](references/ios-readiness-gates.md) for release-specific configuration, package, privacy/dependency, sensitive-data, Apple-requirement, and asset inspection;
- [Candidate evidence and invalidation](references/rc-evidence-and-invalidation.md) for Candidate identity, reproducibility, evidence levels, change impact, Fresh Install applicability, and final binding.

Keep working records light and locatable. Do not create a large gate matrix, Candidate-management system, evidence tracker, release checklist, or parallel project-management surface.

## Define and Preserve the Candidate Baseline

Before relying on evidence, define the current Candidate baseline with at least:

- App version and build;
- Git Source Identity, including repository, branch or detached state, full commit, and relevant dirty diff;
- Bundle ID, target, scheme, and Release Configuration;
- platform, SDK, and destination identity, explicitly distinguishing `iphoneos` from `iphonesimulator`;
- dependency baseline;
- existing Archive identity or an identifiable intended App target + Release Configuration `iphoneos` Release build product;
- applicable support scope;
- relevant Testing evidence and physical-device/human boundaries;
- Trusted Engineering Baseline and Remaining Engineering Risk;
- release-specific verification evidence;
- remaining or explicitly nonblocking deferred evidence.

Investigation may use a dirty working tree. A Final Candidate must not depend on unknown local state: every release-affecting source/configuration change must have an explicit Source Identity, be recoverable from a clear local Git baseline, and exclude unknown or unrecorded release-affecting working-tree changes. Unrelated user files, documents, or untracked material may remain when explicitly shown not to enter or affect the Candidate.

Follow repository rules and protect unrelated work. When task scope is clear, already authorized, and not prohibited, a safe local commit containing only release-affecting task changes may be created without repeatedly asking the user. Never push, force-push, mutate remote branches/tags, merge, upload, publish, or perform another remote mutation without explicit authorization.

## Perform Only Release-Specific Verification

Reuse still-valid Testing Campaign, Final Broad Testing, regression, user real-device, and human physical-device evidence. Do not rerun a Full Discovery Campaign.

Run only checks needed to establish Release confidence, including as applicable:

- build the recorded Release target/configuration;
- install and launch the Candidate where the environment allows;
- run a proportionate core-value-chain Release smoke;
- compare material Release-versus-Debug behavior;
- verify first launch or Fresh Install when release configuration, permissions, caches, migration, persistence, Keychain/container state, or cold start makes it relevant;
- verify release-only permissions, endpoints, flags, logging, resources, output/save/export, lifecycle, or failure surfaces affected by Candidate changes;
- rerun targeted proof and adjacent regression for invalidated behavior evidence.

A Simulator Release build may support Release-mode smoke, Simulator behavior verification, and part of Release-versus-Debug comparison. It cannot by itself serve as the final package/build evidence for Ready. When no existing Archive is available, require at least one Release build product for the intended App target using the Release Configuration and an iOS device destination/`iphoneos` SDK, such as a generic iOS device build. If the environment cannot produce that required product, remain Blocked and name this minimum missing technical evidence.

A successful build is not sufficient. Conversely, this work must not grow into another Testing Campaign. Route behavior verification to `testing` as Delta Testing or Fix Verification when a change can affect product behavior.

## Inspect Release-Specific Engineering Reality

Rely on the Trusted Engineering Baseline; do not perform a mandatory whole-code or Initial Review. Inspect only release-specific engineering surfaces: Release/Debug divergence, build settings, scheme/target, Bundle ID, version/build, `Info.plist`, Entitlements, Capabilities, privacy manifests, extensions, packaged resources, dependency composition, debug/test leakage, secrets/private data, local paths, release endpoints, logging, internal services, and the actual product package.

If the Trusted Engineering Baseline is missing or invalid, route to `code-review`. If this Skill changes source, a dependency, entitlement, capability, build configuration, material resource, or engineering invariant so the baseline changes, route the bounded diff and impact surface to `code-review` Change Review. Do not run Initial Review here.

Verify that source intent equals the actual Release product. Source search, project-file inspection, and symbol or string scans are useful prechecks; they are not by themselves proof of package contents or runtime behavior.

## Run the Objective Release-Defect Loop

Fix a release-specific objective defect directly when the correction is clear, safe, within confirmed intent, and limited to release configuration or packaging—for example a wrong Bundle ID reference, missing packaged resource, incorrect usage description, leaked debug flag, wrong Release endpoint, or approved-asset integration error.

For every Candidate-affecting fix:

1. establish the defect and smallest correct fix;
2. identify what changed and which evidence became stale;
3. route product-behavior impact to `testing` Delta Testing / Fix Verification;
4. route engineering-baseline impact to `code-review` Change Review;
5. perform both routes when both confidence layers changed;
6. rebuild and reinspect the Candidate as needed;
7. rerun targeted release proof and a proportionate Release smoke;
8. bind only current evidence to the next Candidate revision.

Do not clear all evidence mechanically and do not carry old evidence forward automatically. Ordinary development commits do not require elaborate Candidate lineage.

## Verify Dependencies, Privacy, Sensitive Data, and Assets

Inspect dependencies and SDKs actually included in the Release product, their runtime purpose, material release risk, privacy-relevant behavior, manifests/declarations, and consistency with user-facing privacy statements. Inspect the package for private media/data, credentials, local paths, debug/test material, internal services, and excess logging.

The strongest privacy conclusion is **“Privacy behavior and disclosure consistency check passed.”** Never claim legal compliance.

Check already approved/completed App icon, screenshots, privacy URL, support URL, required product-page assets, and App Preview decision where relevant for existence, location, technical usability, Candidate match, sensitive content, and correct integration/reference. Do not redesign them. A missing submission-required asset is Blocked until its owning workflow completes it.

When App Store rules, SDK privacy requirements, supported SDK/Xcode requirements, submission prerequisites, signing behavior, or platform policy may have changed, consult current first-party Apple documentation during execution. Prefer `developer.apple.com`, App Store Connect Help, and other Apple sources; record title/URL and check date. Do not rely on model memory or third-party summaries as authority.

## Label Physical-Device and Human Evidence Truthfully

Use only the level actually proven:

- simulator verified;
- Release product inspected;
- physical-device install verified;
- physical-device launch verified;
- physical-device behavior verified;
- human physical-device UX verified;
- Deferred / Missing.

Reuse credible physical-device evidence when the Candidate has not changed the relevant behavior. If a change invalidates it, require refreshed evidence. Do not pretend a submission-blocking technical check is deferrable merely because the agent cannot operate a physical device; complete all agent-operable work, then ask the user for the smallest necessary action.

## Freeze and Decide

Freeze the Final Candidate only after all required release-specific checks pass and all bound evidence matches its exact Source Identity, configuration, product/package identity, and relevant behavior.

The only user-visible terminal statuses are:

- **Ready for Submission Operations** — no Agent-known release blocker; upstream evidence and Trusted Engineering Baseline remain sufficient; required release-specific checks pass; Candidate/configuration/package/privacy/assets agree; an existing Archive or intended App target + Release Configuration `iphoneos` Release product supplies actual build/package evidence; and no required technical evidence is missing.
- **Blocked** — an objective release defect, invalid baseline, stale or missing required evidence, configuration/package/privacy/security blocker, required asset gap, unresolved product decision, or required technical verification prevents safe entry.

Judge remaining risk by whether it invalidates release trust in this Candidate, not severity alone. Defer only a clearly nonblocking item that does not make the Candidate technically untrustworthy or obstruct Submission Operations. Never defer a crash, wrong output, corruption, privacy/security issue, invalid package/configuration, invalid engineering baseline, required technical evidence, or required submission asset merely to reach Ready.

Ready does not mean an Archive was created or validated, or that a build was uploaded, selected in App Store Connect, submitted, approved, published, or downloadable.

## Keep Progress Lightweight

Use the user's language and this small update shape:

```text
### 当前进展

现在在哪：...
已完成：...
发现：...
下一步：...
需要你：无需操作 / 一个真正需要人的动作
```

Do not expose internal gate matrices or make the user manage Candidate/evidence records.

## Return One Concise Final Report

```text
<App Name> 上架前最终检查

结论：
可以进入 App Store 提交流程 | 暂时不建议提交

当前 Candidate：
version/build；source baseline

这次确认了：
- only readiness-relevant facts

这次修复了：
- only release-relevant objective fixes

仍需注意：
- real remaining risk, human action, or nonblocking deferred evidence
- otherwise: 没有发现阻断进入提交流程的问题

下一步：
- enter Submission Operations
- or route the exact task to Testing / Code Review / MVP / asset workflow

技术信息：
Bundle ID；scheme/configuration；platform/SDK/destination；Release product or existing Archive identity；
Trusted Engineering Baseline；key current evidence
```

Do not output a huge checklist. If there is no existing Archive, use an identifiable intended App target + Release Configuration `iphoneos` Release build product and state: **Archive / Validate checks remain for Submission Operations.**

## Preserve the Submission Boundary

This Skill may inspect an existing Archive or an identifiable intended App target + Release Configuration `iphoneos` Release build product. Requiring the device-target product does not pull submission Archive creation, final distribution-signing operations, Validate App, upload, App Store Connect build selection, Submit for Review, publish, or post-release acquisition into this Skill. Those actions remain in Submission Operations and require their own authorization and evidence.
