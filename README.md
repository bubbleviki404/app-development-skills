# GapLab App Development Skills

GapLab App Development Skills is a collection of modular, independently usable Agent Skills for app development.

## What

The collection turns practical app-development collaboration patterns into composable Skills. It is designed to be modular, composable, and risk-based rather than a universal SOP: invoke each Skill independently when its capability is relevant.

## Skills

### [`ship-real-mvp`](skills/ship-real-mvp/)

Take over an existing app and move it toward the smallest runnable, evidence-aware MVP loop.

### [`adapt-ui-from-references`](skills/adapt-ui-from-references/)

Analyze visual references, calibrate one high-fidelity core screen, then expand from that baseline.

### [`code-review`](skills/code-review/)

Verify engineering risks, repair safe findings, and establish or update a trusted engineering baseline.

### [`testing`](skills/testing/)

Run risk-driven real-app testing and independently verify fixes.

### [`ios-release-readiness`](skills/ios-release-readiness/)

Verify one exact iOS Release Candidate before submission operations.

### [`ios-submission-ops`](skills/ios-submission-ops/)

Guide a Ready Final Candidate through Apple submission operations to verified Waiting for Review closeout.

## Architecture

Each Skill is an independently maintainable bundle. Projects can use only the bundles relevant to their needs; no universal pipeline is required.

## Install / Use

Each directory under `skills/` is a Skill bundle. On a host that supports Agent Skills, use that host's import or installation mechanism to install or import the directory. This repository does not assume a universal installation path.

When the host supports explicit Skill invocation, use `$ship-real-mvp`, `$adapt-ui-from-references`, `$code-review`, `$testing`, `$ios-release-readiness`, or `$ios-submission-ops`.

Example uses:

- Use `$ship-real-mvp` to take over an existing app and continue from its current reality.
- Use `$adapt-ui-from-references` to turn visual references into one calibrated core screen before scaling the UI.
- Use `$code-review` to verify engineering risks and establish or update a trusted engineering baseline.
- Use `$testing` to discover product bugs through risk-driven real-app coverage or independently verify a fix.
- Use `$ios-release-readiness` to inspect one exact iOS Release Candidate before submission operations.
- Use `$ios-submission-ops` to guide a Ready Final Candidate through submission operations and verified Waiting for Review closeout.

## Status

This repository currently contains six public Skill bundles:

- `ship-real-mvp`
- `adapt-ui-from-references`
- `code-review`
- `testing`
- `ios-release-readiness`
- `ios-submission-ops`

The Skills are usable as independent bundles. Validation depth varies by Skill; see the individual Skill documentation and repository history for their current scope and limitations.

## Limitations

- Validation depth varies across Skills.
- The published Skills are not claimed to be production-proven in every environment.
- Optional specialist routes may have less direct validation.
- Host support for Agent Skills and explicit Skill invocation varies.

## License

This repository and the included Skill bundles are licensed under the MIT License. Copyright (c) 2026 GapLab. See [`LICENSE`](LICENSE).

See [`CHANGELOG.md`](CHANGELOG.md) for repository and Skill history.
