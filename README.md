# GapLab App Development Skills

GapLab App Development Skills is a curated public release repository for a modular collection of App Development Skills.

## What

The collection organizes collaboration patterns observed and validated through real App development into composable Skills. The goal is not one universal SOP. The intended shape is modular, composable, and risk-based: each Skill can be invoked independently when its capability is relevant.

This repository is a curated public release channel, not a backup of a local working directory and not a second local source of truth. The normal direction is:

```text
Local Working Skills → Curated Public Skills → Stable Public Release
```

The local working source is inspected, validated, and curated here. Future version promotion and formal release decisions remain Human-controlled.

## Skills

### [`ship-real-mvp`](skills/ship-real-mvp/)

Take over an existing app and move it toward the smallest runnable, evidence-aware MVP loop.

### [`adapt-ui-from-references`](skills/adapt-ui-from-references/)

Analyze visual references, calibrate one high-fidelity core screen, and expand only after the visual baseline is approved.

### [`code-review`](skills/code-review/)

Verify engineering risks, repair safe findings, and establish or update a trusted engineering baseline.

### [`testing`](skills/testing/)

Run coverage-driven real-app testing across product surfaces and risk dimensions, and independently verify implemented fixes.

### [`ios-release-readiness`](skills/ios-release-readiness/)

Verify one exact iOS Release Candidate and decide whether it can safely enter App Store Submission Operations.

### [`ios-submission-ops`](skills/ios-submission-ops/)

Guide one Ready Final Candidate through Apple Developer, App Store Connect, Archive, Validate, Upload, Submit for Review, and verified Waiting for Review closeout.

Each Skill is an independent bundle. Choose only the Skills relevant to your project; new Skills are listed here only after they are publicly curated in this repository.

## Architecture

Each Skill remains an independently maintainable unit. Projects can use only the public bundles relevant to their needs; the repository does not require a universal pipeline.

## Status

**Repository Published · `ship-real-mvp`, `adapt-ui-from-references`, `code-review`, `testing`, `ios-release-readiness`, and `ios-submission-ops` Public Release Candidates**

This GitHub repository is public. `ship-real-mvp` remains a Public Release Candidate based on one bounded direct real-App pilot, and its Human Packaging Review has passed. `adapt-ui-from-references`, `code-review`, `testing`, `ios-release-readiness`, and `ios-submission-ops` are Public Release Candidates based on their curated public bundles; no Skill is declared Released v1.0 here. The capabilities are not production-proven. Future version promotion, tags, GitHub Releases, package publication, and other release actions remain Human-controlled.

## Install / Use

Each directory under `skills/` is a distributable Skill bundle. On a host that supports Agent Skills, use that host's Skill import or installation mechanism to install or import the directory. This repository does not assume a universal installation path.

Invoke `$ship-real-mvp`, `$adapt-ui-from-references`, `$code-review`, `$testing`, `$ios-release-readiness`, or `$ios-submission-ops` where the host supports explicit Skill invocation.

Example uses:

- Use `$ship-real-mvp` to take over an existing app and continue from its current reality.
- Use `$ship-real-mvp` to turn a prototype into the smallest runnable product loop.
- Use `$ship-real-mvp` to continue a runnable MVP without restarting valid product discovery.
- Use `$adapt-ui-from-references` to turn visual references into one calibrated core screen before scaling the UI.
- Use `$code-review` to verify engineering risks, repair safe findings, and establish or update a trusted engineering baseline.
- Use `$testing` to discover product bugs through risk-driven real-app coverage or independently verify an implemented fix.
- Use `$ios-release-readiness` to inspect one exact iOS Release Candidate and decide whether it can enter submission operations.
- Use `$ios-submission-ops` to guide a Ready Final Candidate through submission operations and verified Waiting for Review closeout.

Each listed bundle is usable on its own. Additional Skills will be listed here only when they become public components.

## Limitations

- Current evidence includes one bounded direct real-App pilot.
- The published capabilities are not production-proven.
- Not every optional specialist route has direct validation.
- Future version promotion, tags, GitHub Releases, and other release actions remain Human-controlled.

## Scope and boundaries

- Local working Skills remain maintained in their local source of truth.
- This repository contains only curated public material approved for this channel.
- A local file, successful execution, benchmark, or public repository copy does not by itself prove production maturity or public release readiness.
- Private project names, credentials, personal data, session identifiers, machine-specific paths, third-party media, and unclear-license material require review before inclusion.

## License

The repository and the packaged Skills use the MIT License, with `Copyright (c) 2026 GapLab`. This reflects the Human ownership decision for the current packages; future third-party additions require a new review.

See [`CHANGELOG.md`](CHANGELOG.md) for public repository and Skill history.
