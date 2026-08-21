---
name: adapt-ui-from-references
description: Reference-led UI/UX production workflow that atomically analyzes screenshots, assigns cross-reference layer ownership, and calibrates one high-fidelity core state before scaling. Use when designing or implementing an app from one or more reference images, choosing independently between light/medium/heavy product discussion and HTML/Figma/direct-code output, preventing colored-wireframe results, or adapting an approved visual baseline across more states without copying source-product semantics.
---

# Adapt UI From References

Extract a traceable design direction from references, prove it on one real core state, and expand only after the user approves the visual baseline. Optimize for a usable app impression before board completeness or design-system completeness.

## Confirm Two Independent Axes

Ask only when the user has not already decided.

1. Confirm **discussion intensity**:
   - **Light:** problem, core task, decisive constraints, and open choices.
   - **Medium:** also IA, meaningful states, risks, and edge cases.
   - **Heavy:** also alternatives, tradeoffs, dependencies, and system effects.
2. Confirm **output route** separately:
   - **Interactive HTML**
   - **Editable Figma**
   - **Direct target code**, such as Swift/SwiftUI or the requested framework

Never infer output route from discussion intensity. Respect an explicit route. Otherwise recommend:

- one interactive high-fidelity HTML core screen when references drive the direction and visual realism is the main uncertainty;
- one editable Figma core screen when the user explicitly needs manual visual editing;
- direct target code when the visual direction is already clear and native behavior is the main uncertainty.

Before design or implementation, ask whether reference images exist unless the user already supplied or explicitly declined them.

## Establish The Target

Record the target product, primary user task, platform, one representative core state, essential interaction, constraints, and non-goals. The target owns UX, IA, business logic, content, accessibility, and platform behavior.

## Analyze References Before Producing UI

When references exist:

1. Create one **Atomic Reference Record** per image: visible facts, labeled UX inference, transferable signals, rejected source semantics, and uncertainty.
2. Classify cross-image relationships: same-family, complementary, conflicting, or unrelated.
3. Assign explicit layer ownership for UX/IA, layout, typography, color, surface, components, imagery, and state/motion behavior. Never merge sources as an undifferentiated union.
4. Compose only adopted signals into one **Style Route**.
5. Write a **Target Adaptation Contract** for the target-owned state, behavior, layout, content, provenance, rejections, and open decisions.

If no references exist, proceed target-first and never invent reference provenance. Read [references/workflow.md](references/workflow.md) when exact compact artifact fields or gate checks are needed.

## Pass The Visual Calibration Gate

Before building multiple screens, variables, a component library, or a design system:

1. Select the single state that best represents real use and the unresolved visual direction.
2. Produce that state at high fidelity through the chosen route, including its essential interaction when the route supports interaction.
3. For media-led products, use real user-provided or credible task-relevant media first. Never present abstract gradients, rectangles, or generic geometry as a high-fidelity substitute for camera, video, photo, map, product, or content surfaces.
4. Make the result immediately perceptible as a plausible real app, not a colored wireframe.
5. Run the Realness Gate, present the result, and request explicit direction approval.

Keep the initial calibration scope to one core object/state. Iterate on that same baseline as needed until it passes the gate or the user approves it. The limit applies to expanding or copying an unapproved direction, not to the number of necessary refinements.

## Run The Realness Gate

Check the core state for:

- real or credible content and correct media crop, aspect ratio, and focal treatment;
- platform safe areas and a native-appropriate control density;
- coherent material, contrast, depth, and visual hierarchy;
- usable touch targets and unambiguous primary action;
- visible feedback for the essential interaction and meaningful state change;
- adopted reference signals with clear provenance and no source-product contamination.

Reject the result as a **colored wireframe** if color is doing the work while content, media, material, hierarchy, or interaction remains schematic. Fix the core state before expanding.

## Respond To User Feedback

Treat an approved or nearly approved core state as the baseline. Apply requested micro-adjustments—layout, media treatment, control size, copy, material, color, or interaction—on that baseline first. Do not restart or replace the direction unless the user rejects it or the change invalidates the Style Route or Target Adaptation Contract.

Expand only after explicit approval.

## Expand Deliberately

After approval:

- extend the baseline to contracted states in priority order;
- componentize repeated, stateful, or high-change elements only when reuse is demonstrated;
- add Figma variables/components or a broader design system from the approved visual baseline, not before it;
- preserve the chosen media treatment, hierarchy, platform density, and interaction language.

For Figma, do not create a complete variables library, component library, or multi-screen board before the core screen is confirmed. Keep the calibration screen editable; componentize it after approval.

## Run Contract Coverage Check

Whenever states or screens are expanded, compare every contracted frame/state against the actual output. Record each as `implemented`, `intentionally deferred`, or `blocked`. Do not claim completion while any contracted item is missing or unaccounted for.

## Keep Cost And Evaluation Outside The Core

- Limit the first round to one core screen/state and one visual calibration.
- Do not multiply an unapproved direction across screens.
- Do not run Builder/Evaluator/Sealer roles, blind scoring, evidence sealing, or multi-role release review.
- Leave product and accessibility review to the later GapLab release workflow.

If browser execution, screenshot capture, simulator access, or visual inspection is unavailable, disclose the limitation. Perform available static checks on structure, scripts, assets, and state coverage, then ask the user to open the artifact. Never claim that visual testing passed without seeing the rendered result.
