# Compact Artifacts And Gates

Read this file only when exact fields are useful. Keep artifacts proportional to the selected discussion intensity.

## Atomic Reference Record

```text
Source: stable image label
Observed: visible facts only
UX inference: plausible intent, labeled as inference
Transferable: layout / type / color / surface / component / imagery / state
Reject: brand, semantics, navigation, assets, or controls that cannot transfer
Confidence: high / medium / low, with uncertainty
```

## Relationship And Ownership

For each pair, label `same-family`, `complementary`, `conflicting`, or `unrelated`. Then assign one owner per relevant layer:

```text
Target: UX / IA / logic / content / accessibility / platform behavior
Reference A: specific visual layers or regions
Reference B: specific visual layers or regions
Inactive this scope: retained for later, not visible now
Rejected: forbidden transfer
```

Escalate unresolved conflicts to the user. Do not average them.

## Style Route

```text
Route statement
Active foundations: type / color / spacing / radius / surface / elevation
Layout and media rules
Component and control language
State and interaction language
Active vs inactive reference signals
```

## Target Adaptation Contract

```text
Target goal and primary task
Platform and output route
Calibration state and essential interaction
Target-owned IA and behavior
Layout zones and real-content requirements
Adopted signals with provenance
Rejected signals and non-goals
Future frames/states, clearly deferred until approval
Open decisions
```

Do not pre-specify a full token library or exhaustive component inventory for the calibration state.

## Visual Calibration Gate

Proceed to user review only when all are true:

- exactly one representative core state is the main first-round artifact;
- task-relevant media/content is present and correctly cropped;
- safe areas, control density, hierarchy, material, and touch targets are credible;
- the essential interaction works or is represented honestly for the selected route;
- the output reads as a real product surface rather than a styled schematic;
- adopted and rejected reference signals remain traceable.

If a check fails, keep refining this same state until it passes or the user approves it. Do not add screens to compensate; the constraint is one calibration object, not one revision.

## Route-specific first output

- **HTML:** one responsive core surface with real media, the essential interaction, and a user-openable entry point. Prefer this when visual direction is uncertain and editability in Figma is not required.
- **Figma:** one editable high-fidelity core frame and only the components necessary to edit that frame. Do not build the full library or screen set yet.
- **Direct code:** one runnable native/target-platform core state with the essential native behavior. Use when the design direction is already understood.

## Feedback And Expansion

After feedback, patch the approved baseline first. Re-run the Realness Gate for material visual changes. Expand only after explicit direction approval.

When expanding, keep a coverage table:

| Contract frame/state | Actual artifact | Status | Note |
|---|---|---|---|
| name | link/path/node | implemented / deferred / blocked | reason or verification |

Completion requires every contracted item to have a status. A missing row is a coverage failure.

## Honest verification

When rendered visual inspection is unavailable, report exactly which static checks ran, such as file existence, script syntax, asset references, interaction wiring, or contract coverage. Label visual quality as unverified and give the user the path or instructions to open it.
