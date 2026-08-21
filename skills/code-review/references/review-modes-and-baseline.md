# Review Modes and Trusted Baseline

## Initial Review

Use when no credible Trusted Engineering Baseline exists, the baseline is unknown or stale, ownership/history is unclear, or a first formal engineering review follows an MVP.

Review enough of the core product path and engineering shape to identify systemic risk. Prioritize high-risk ownership, lifecycle, state, async/concurrency, persistence, data/resource, and test-truth paths. Do not define completion as scanning every file.

Complete when:

- Source Identity is explicit;
- the core product path and critical engineering structure are sufficiently understood;
- material high-risk paths were reviewed;
- verified findings are resolved, or accepted/deferred only when they do not invalidate engineering trust in the declared baseline scope;
- any baseline-blocking Scoped Rescue is complete;
- relevant engineering regression has evidence;
- `ENGINEERING.md` matches current material truth;
- remaining risks and the next review starting point are explicit.

## Change Review

Use only with a credible baseline. Begin with:

`Current Diff + Impact Surface + Related Ownership + Related State + Related Rules + Related Tests`

Do not restart Initial Review for each small change. Remaining risk alone does not justify global review. Expand scope or explicitly re-enter Initial Review only when evidence shows the Trusted Baseline is invalid, material systemic risk exists outside the reviewed impact surface, ownership/lifecycle/data/concurrency changes cross the current baseline, or the current change can no longer safely rely on that baseline.

Complete when the baseline is known, the diff and impact surface are understood, verified findings are resolved or accepted/deferred only under the non-invalidating rule below, regression passes, and no evidence invalidates the unreviewed baseline.

## Scoped Rescue

Enter only for a verified systemic mechanism that a local fix cannot remove. Define the affected subsystem, invariants to restore, allowed changes, excluded areas, regression boundary, and stop condition before broad edits.

Never use Rescue as permission to rewrite the whole architecture. Finish when before/after evidence proves risk reduction, not when the code looks cleaner.

## Continue the Current Review Mode

When meaningful risk remains:

- Initial Review continues risk-driven review;
- Change Review continues diff plus impact-surface review;
- Scoped Rescue continues its current rescue and verification boundary.

Do not treat remaining risk as an automatic return to Initial Review. Apply the explicit scope-expansion conditions above.

## Trusted Engineering Baseline

Keep the baseline lightweight. Compose it from:

1. repository, branch, full `HEAD`, and `HEAD + current working tree` when dirty;
2. current `ENGINEERING.md`;
3. latest Code Review Report;
4. exact build/test/regression evidence;
5. accepted and deferred engineering risks with resume conditions when known.

Do not create `BASELINE.json`, a dashboard, or a health score.

Use only these decisions:

- **Established** — Initial Review completion evidence is sufficient.
- **Updated** — Change Review completion evidence is sufficient and the prior baseline remains credible outside the reviewed impact surface.
- **Not Ready** — An unresolved risk invalidates engineering trust within the declared baseline scope, a baseline-blocking Rescue remains incomplete, Source Identity is untrusted, engineering truth is contradictory, or regression evidence is inadequate.

Accepted and Deferred Engineering Risks may coexist with an Established or Updated baseline only when they do not materially compromise correctness, ownership/lifecycle integrity, state authority, data/resource integrity, or safe-change confidence within the declared scope. Examples include unproven physical-device performance pressure, a bounded low-risk future optimization, or deferred evidence outside the scope that does not affect current trust.

They cannot coexist with a trusted decision when the unresolved mechanism still makes the reviewed source untrustworthy, such as confirmed late-result state writes, data-corruption risk, core ownership ambiguity that can produce wrong behavior, evidence that current modification cannot continue safely, or incomplete baseline-blocking Rescue.

Ask: **Does this unresolved risk invalidate engineering trust in the declared baseline scope?** If yes, choose **Not Ready** regardless of whether the finding is marked `Accepted Risk` or `Deferred`. If no, retain the baseline and record the Remaining Engineering Risk. Do not block mechanically by severity alone.

State the narrow scope of trust. Never convert a baseline decision into a whole-repository health certificate, product-testing result, or release approval.

## Integration Interface

Accept current source and product state, `PRODUCT.md`, `ENGINEERING.md`, the Testing handoff and known accepted/deferred risks, and existing baseline evidence.

Output Review Mode, Source Identity, verified findings, suspected risks, repair/Rescue status, engineering regression evidence, remaining risk, Trusted Baseline decision, and next route: Release Readiness, Continue Rescue, Testing Delta, or Product Decision Required.
