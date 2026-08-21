# iOS Release-Specific Readiness Checks

Use these prompts by applicability and release risk. They are not a mandatory matrix, a second Testing Campaign, or a whole-code review.

## Release Configuration and Actual Product

Tie one identifiable Release product or existing Archive to its recorded source and inspect both intent and actual contents:

- App version/build, Bundle ID, target, scheme, Release Configuration, and platform/SDK/destination identity, explicitly distinguishing `iphoneos` from `iphonesimulator`;
- `Info.plist`, usage descriptions, Entitlements, Capabilities, extensions, privacy manifests, and signing-related configuration that can be inspected before Submission Operations;
- included resources, App icon integration, frameworks, dependencies, embedded content, and localized material;
- Release/Debug compilation conditions, feature flags, endpoints, services, diagnostics, logging, and failure behavior;
- debug/test assets, fixtures, secrets, personal identifiers, private media/data, absolute local paths, internal services, and development-only resources that must not enter the package.

Compare source intent with the built product. Project-file review, `grep`, symbol scans, or source presence are prechecks, not sufficient package proof.

An existing Archive may supply the actual build/package evidence when its identity is bound to the Candidate. When no Archive exists, Ready requires at least one product from the intended App target + Release Configuration built for an iOS device destination/`iphoneos` SDK, such as a generic iOS device build. A `Release-iphonesimulator` product alone is insufficient; if the required `iphoneos` product cannot be formed, remain Blocked and state this minimum missing evidence.

When only the required `iphoneos` Release build product exists, inspect it and state that submission Archive creation, final distribution-signing operations, and Archive/Validate checks remain for Submission Operations. Never imply that an Archive was verified.

## Release-Mode Behavior

Use current upstream Testing evidence, then run only proportionate checks that establish the Candidate's Release-specific truth:

- Release build, install, and launch where the environment permits;
- core-value-chain smoke with representative input;
- material Release-versus-Debug differences;
- first launch or Fresh Install when permissions, persisted state, migration, caches, Keychain/container state, cold start, or release-only configuration can affect the result;
- allow/deny/recovery and Settings paths affected by permission, entitlement, or usage-description changes;
- output, save, export, lifecycle, recovery, or failure paths invalidated by Candidate changes;
- targeted runtime proof for dependency, build-setting, resource, endpoint, or package changes.

A Simulator Release product may support Release-mode smoke, Simulator behavior verification, and part of Release-versus-Debug comparison. Do not promote that evidence into final package/build proof for Ready.

Do not mechanically repeat Full Discovery. Route product behavior that needs independent verification to `testing` Delta Testing / Fix Verification.

## Release-Specific Engineering Inspection

Rely on a valid Trusted Engineering Baseline. Inspect the release boundary rather than the whole codebase:

- Release/Debug divergence and conditional behavior;
- scheme, target, build settings, configuration sources, Bundle ID, version/build, and packaged resources;
- Entitlements, Capabilities, privacy manifests, extensions, frameworks, and dependency composition;
- release endpoints, flags, accounts, local paths, logging, debug/test leakage, sensitive data, and secret exposure;
- discrepancies between approved source/configuration and the actual product.

Route a missing or invalid baseline to `code-review`. Route source, dependency, entitlement, capability, build-configuration, material-resource, or engineering-invariant changes to Change Review when they alter the baseline.

## Dependencies, Privacy, and Sensitive Data

For dependencies and SDKs actually included:

- identify version/baseline, runtime purpose, initialization, invoked capabilities, and material release/distribution risk;
- inspect privacy-relevant access, manifests/declarations, data flow, endpoints, and failure behavior;
- compare package/source behavior with current user-facing privacy statements;
- verify that private user material, test accounts/data, credentials, local paths, internal services, and excess logs are absent from the Release product.

Allowed conclusion: **Privacy behavior and disclosure consistency check passed.** Do not claim legal compliance.

## App Store Asset Readiness

For approved/completed assets and support information, confirm:

- App icon, screenshots, privacy URL, support URL, required localized/product-page assets, and App Preview decision where applicable exist and are locatable;
- files and URLs are technically usable for their intended submission step;
- content and integration match the Candidate and do not expose private or sensitive information;
- package/project references point to the approved asset and do not include unintended alternatives.

Fix an objective integration/reference/format defect when the approved source is known. Do not redesign creative work. Route unfinished assets to their owner. Treat any missing submission-required asset as Blocked.

## Mutable Apple Requirements

At execution time, consult current first-party Apple documentation for mutable requirements such as App Store rules, supported SDK/Xcode versions, SDK privacy requirements, submission prerequisites, signing behavior, and platform policy.

Prefer `developer.apple.com`, App Store Connect Help, and other official Apple sources. Record the page title, URL, check date, and the Candidate decision it supports. Treat cached knowledge, third-party checklists, blogs, and search snippets only as leads. If official guidance is unavailable or ambiguous, state the uncertainty and route the smallest necessary decision instead of guessing.
