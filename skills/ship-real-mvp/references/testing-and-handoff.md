# Testing and Handoff

This reference defines the main Skill's bounded testing interface. It is not a replacement for a dedicated Testing capability.

## Builder Self-Test

Before asking a user to test, build and run the product where possible. Exercise accessible actions, meaningful states, outputs, key screens, affected developer checks, and the complete path available in the current environment.

Compilation, unit-test success, installation, launch, or a simulator check is only evidence of that specific surface. It is not automatically complete product testing or physical-device UX proof.

Record physical-device, hardware, sensory, inaccessible system UI, permission, or other human-only boundaries as Deferred / Human Evidence.

## Testing Entry

Use an independent Testing capability when behavioral risk, a confirmed Bug, a meaningful change, or a stabilization pass makes it useful. Provide only:

- current product/build and source identity;
- relevant scope or change;
- environment constraints;
- still-valid prior evidence;
- requested mode, such as discovery, delta testing, or fix verification.

Do not require a particular private tool, tracker, campaign format, or internal report schema.

## Public Handoff Output

Consume only the public handoff:

- what ran and did not run;
- Testing mode and session/campaign status, if provided;
- findings or confirmed Bugs;
- coverage and remaining risk;
- verification result;
- blocked, deferred, or human evidence;
- next action and the narrow claim supported.

The main Skill owns routing and claim interpretation. The Testing capability owns its own execution method, findings, and independent fix-verification authority.

## Bounded Fallback

If an independent Testing capability is unavailable, perform only lightweight active checks appropriate to the risk and state clearly: `Dedicated Testing capability unavailable`. Do not call the fallback a complete Testing Campaign, and do not recreate a second campaign system.

## Bug and Feedback Loop

For a confirmed Bug: preserve reproduction evidence, implement and developer-check the fix, then return to independent product-behavior verification when available. A code change alone is `Implemented`, not `Fixed`.

Classify user feedback as an objective Bug, product behavior/scope change, or UX/UI preference. Route each through the corresponding implementation and proportionate regression path.

## Claim Narrowing

Never promote a lower evidence level into a higher one. A successful build is not a working product claim; a simulator result is not a physical-device claim; a local release check is not distribution verification; an unavailable specialist is not a passed specialist.
