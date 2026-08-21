# Engineering Alignment

Use this reference before substantial implementation or when a change could affect shared behavior, data, lifecycle, platform support, or verification confidence.

## Decide the Smallest Safe Shape

Reason continuously from value and scope to build order, structure, impact, and verification. Prefer the simplest clear architecture that fits the real risk. Add an abstraction only when there is a repeated semantic rule, multiple consumers, a lifecycle or platform boundary, a testability need, or a real change-safety problem.

## Engineering Boundaries to Make Explicit

Record only decisions relevant to the product:

- system shape and responsibility ownership;
- source of truth and data lifecycle;
- files, media, resources, and cleanup;
- async work, cancellation, stale results, and recovery;
- platform, device, localization, accessibility, and support range;
- privacy-sensitive areas and permission behavior;
- deterministic logic and how it is tested;
- current constraints and deliberate tradeoffs.

Handle real corruption, data loss, concurrency, permission, cancellation, privacy, and platform failure modes. Do not add substantial machinery for hypothetical scenarios without a credible risk.

## Minimal Engineering Memory Contract

Create or maintain a compact `ENGINEERING.md` when it helps future work recover engineering truth:

```markdown
# [Product] — Engineering

## System Shape
## Ownership and Lifecycle
## Platform and Support
## Data / Files / Async / Recovery
## Testing Strategy and Verification Boundary
## Privacy-Sensitive Areas
## Current Constraints and Deliberate Tradeoffs
```

The file is not a full architecture handbook, dependency graph, component catalogue, CI design, Bug report, or specialist review report.

## Change and Verification

For a material change, identify the affected surface and run the smallest checks that can prove it, plus a proportionate main-path regression. Reuse evidence while the source and configuration remain the same; reassess evidence freshness after changes that invalidate it.

Update `ENGINEERING.md` when architecture shape, ownership, lifecycle, data flow, concurrency, platform boundary, or testing strategy materially changes.
