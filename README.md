# GapLab App Development Skills

GapLab App Development Skills is a curated public release repository for a modular collection of App Development Skills.

## What

The collection organizes collaboration patterns observed and validated through real App development into composable Skills. The goal is not one universal SOP. The intended shape is modular, composable, and risk-based: each Skill can be invoked independently when its capability is relevant.

This repository is a curated public release channel, not a backup of a local working directory and not a second local source of truth. The normal direction is:

```text
Local Working Skills → Curated Public Skills → Stable Public Release
```

The local working source is inspected, validated, privacy/provenance/dependency-audited, and then curated here. External publication remains a separate Human decision.

## Architecture

Each Skill remains an independently maintainable unit. The future suite will describe how the units relate, while avoiding a mandatory waterfall pipeline. A conceptual map may include:

```text
Idea / Requirement
        ↓
Product shaping and MVP delivery
        ↓
Reference-led UI calibration (when visual references matter)
        ↓
Implementation and engineering review
        ↓
Testing and fix verification
        ↓
Release readiness
        ↓
Submission operations (when explicitly required)
```

Projects may enter, skip, or revisit these capabilities according to evidence and risk. The suite organizes relationships; it does not require every project to execute every stage.

## Status

**Public Release Candidate / Human Packaging Review passed**

This repository is not a production-proven suite. `ship-real-mvp` has a packaged public release candidate based on one bounded direct real-App pilot, and its Human Packaging Review has passed. No Skill is declared Released v1.0 here, and external publication remains a separate Human-controlled decision. The public records describe the package's evidence boundary, maturity, and safety limitations.

## Install / Use

`skills/ship-real-mvp/` is a distributable Skill bundle. On a host that supports Agent Skills, use that host's Skill import or installation mechanism to install or import the directory. This repository does not assume a universal installation path.

Invoke `$ship-real-mvp` where the host supports explicit Skill invocation.

Example uses:

- Use `$ship-real-mvp` to take over an existing app and continue from its current reality.
- Use `$ship-real-mvp` to turn a prototype into the smallest runnable product loop.
- Use `$ship-real-mvp` to continue a runnable MVP without restarting valid product discovery.

Testing, Code Review, Release Readiness, and Submission Operations are optional specialist integrations. The core capability remains usable without installing any of them.

## Limitations

- Current evidence includes one bounded direct real-App pilot.
- The capability is not production-proven.
- Not every optional specialist route has direct validation.
- External release and publication remain Human-controlled.

## Scope and boundaries

- Local working Skills remain maintained in their local source of truth.
- This repository contains only curated public material approved for this channel.
- A local file, successful execution, benchmark, or public repository copy does not by itself prove production maturity or public release readiness.
- Private project names, credentials, personal data, session identifiers, machine-specific paths, third-party media, and unclear-license material require review before inclusion.

## License

The repository and the packaged `ship-real-mvp` candidate use the MIT License, with `Copyright (c) 2026 GapLab` recorded in the package provenance. This reflects the Human ownership decision for the current package; future third-party additions require a new review.

See [`skills/ship-real-mvp/PROVENANCE.md`](skills/ship-real-mvp/PROVENANCE.md), [`VERSION_MANIFEST.md`](VERSION_MANIFEST.md), and [`CHANGELOG.md`](CHANGELOG.md) for the current candidate status and release history.
