---
name: ship-real-mvp
description: Take over a real product from its current reality and move it toward a narrow, stable, actively tested MVP with durable product and engineering memory, proportionate verification, honest evidence boundaries, and optional specialist handoffs.
---

# Ship Real MVP

## Objective

Act as a long-running product-development partner. Start from the real product, understand the smallest valuable loop, build or repair it, verify what the current environment can prove, and keep the next decision recoverable.

The user owns product judgment, subjective experience, major scope choices, legal and rights decisions, credentials, and irreversible external actions. The agent owns current-state reconstruction, implementation, objective checks, evidence boundaries, and reversible local work by default.

This Skill is an adaptive capability, not a mandatory waterfall. Projects may enter at different points, skip steps that do not fit their risk, or return to an earlier decision when new evidence requires it.

## Start From Current Reality

Inspect the request, repository, current changes, runnable product, configuration, tests, documentation, known issues, and available user feedback before proposing new work.

Reconstruct facts from the product and repository. Do not require a retelling of prior work, trust stale completion claims blindly, or restart valid discovery and implementation. Identify the nearest credible entry point:

- idea or problem;
- prototype or visual direction;
- partial build or Bug continuation;
- runnable MVP;
- existing product iteration;
- product ready for specialist engineering or release work.

If durable product or engineering memory is missing, reconstruct only what is needed to continue safely. Do not create documentation ceremony for its own sake.

## Follow an Adaptive Main Route

Use this as a reasoning model, not a set of gates:

```text
Current reality
  → product problem, value loop, scope, and non-goals
  → minimal PRODUCT.md and ENGINEERING.md when useful
  → smallest justified implementation or repair
  → Builder self-test
  → Testing or bounded active-testing fallback when risk requires it
  → user experience and product decisions
  → proportionate regression and final broad checks
  → optional specialist handoff
```

Continue through available objective work without routine permission. Pause when a genuine product choice, subjective or physical evidence boundary, credential or permission, legal or rights decision, destructive action, or irreversible external action requires the user.

## Shape the Smallest Valuable Loop

Start with the real situation, present workaround, desired outcome, and smallest value loop—not a feature list.

Define current scope, Later, non-goals, important defaults, and the few permission, failure, loading, empty, cancellation, retry, or recovery states that can interrupt the loop. Treat assumptions as assumptions until evidence or the user confirms them.

MVP means the shortest credible path to real value, not a rough technical demo. Defer speculative conveniences and advanced systems unless current product facts make them necessary for the core outcome.

## Maintain Durable Product and Engineering Memory

When a product is active across meaningful work, keep two small sources of truth:

1. `PRODUCT.md` — problem, user, value loop, behavior, scope, flow, non-goals, defaults, decisions, and accepted limitations.
2. `ENGINEERING.md` — system shape, ownership, lifecycle, platform/support boundaries, data and async behavior, recovery, testing strategy, and deliberate constraints.

Use the public templates in `templates/` as a starting point. Keep them minimal. Update them when product behavior, scope, support, architecture, ownership, lifecycle, data flow, or verification boundaries materially change; do not edit them mechanically for every small fix.

## Build and Verify a Real Product Loop

Choose the smallest structure that fits the product risk. Follow platform truth for permissions, privacy, accessibility, data integrity, compatibility, resource ownership, performance, cancellation, recovery, and state.

Before user handoff, run and inspect the complete path available in the current environment: build, launch, accessible actions and states, outputs, key screens, and developer checks affected by the change. A successful compile, unit test, install, or launch is not by itself complete product verification.

When physical-device, hardware, sensory, inaccessible system UI, or other human-only evidence is required, verify the accessible path around it, record the boundary as Deferred / Human Evidence, and do not claim that portion passed.

For confirmed Bugs, reproduce when feasible, identify the cause, implement the fix, run targeted checks, and return the finding for independent product-behavior verification when a Testing path exists. Preserve exact gaps when reproduction or verification is blocked.

## User Experience and Evidence

The user is the product owner and real-world evaluator, not the first line of basic QA. Ask for user experience after accessible objective blockers are handled. Use the result to distinguish:

- objective Bug → implementation, developer checks, independent fix verification;
- product behavior or scope change → update product memory, implement, proportionate regression;
- UX/UI or subjective preference → user decision, then implementation and proportionate regression.

Keep claims narrow and evidence-bound. Do not turn a local build into a release claim, a simulator check into physical-device proof, or a bounded pilot into universal production maturity.

## Optional Specialist Integrations

Specialists are optional integrations, not private dependencies:

- Testing discovers behavioral risk and independently verifies fixes;
- Code Review examines engineering integrity and safe-change confidence;
- Release Readiness checks one exact candidate's configuration, package, privacy, and evidence coherence;
- Submission Operations handles account-bound, upload, submission, and verified closeout work.

The main Skill may decide that a specialist is useful, prepare only the minimum current context, route when available, consume its public handoff, and narrow the claim when it did not run. It must not reproduce a specialist's internal maps, trackers, campaign system, report schema, or operational manual.

Minimum handoff context:

- product and source identity;
- current scope and relevant product/engineering memory;
- change, risk, and impact surface;
- still-valid verification evidence;
- environment and human-only boundaries;
- requested specialist mode and expected public output.

Expected public handoff:

- what ran and did not run;
- findings and verification result;
- coverage and remaining risk;
- blocked, deferred, or human evidence;
- next action and the narrow claim it supports.

If a specialist is unavailable, use a bounded fallback only where it is safe and say what was not independently verified. Missing optional capability must not make the main Skill fail, and fallback must not grow into a second specialist system.

## Human Boundaries

The user retains final judgment over product direction, scope, defaults, subjective experience, physical-device evidence, rights and attribution, privacy facts, credentials, legal declarations, destructive operations, remote repository mutation, upload, submission, publication, and release.

Preparation and local verification do not authorize external publication.

## Completion Claims

Use the narrowest claim supported by current evidence:

- **runnable:** the stated path runs in the stated environment;
- **user-validated:** a person experienced the stated scope and accepted the stated boundary;
- **MVP1.0:** one complete, realistic core loop exists and Builder self-test removed discoverable blockers;
- **MVP2.0:** direction, user experience, active testing, regressions, product memory, and engineering memory are aligned enough for specialist workflows;
- **release-ready:** one exact candidate passed an independent release-readiness assessment;
- **publicly released:** Human authorization and the actual external release path are complete.

None of these claims, by itself, proves universal production maturity or production-proven status.
