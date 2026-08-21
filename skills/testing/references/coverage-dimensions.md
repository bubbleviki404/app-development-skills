# Relevant Coverage Dimensions

Use these dimensions as a relevance prompt, not a fixed case list. For a Full Discovery Campaign, consider every dimension, then assign `Covered`, `Partial`, `Not Covered`, `Blocked`, or `N/A`. Give N/A a reason. Add product-specific dimensions when the product has risks not represented here.

## Contents

- Core Journey
- Negative / Failure
- Boundary
- State Transition
- Rapid / Repeated / Abuse
- Race / Async
- Lifecycle
- Persistence / Recovery
- Device / Adaptation
- Accessibility
- Hardware / Platform-specific
- Stress / Performance
- Data Integrity
- Privacy / Destructive Behavior

## Core Journey

Execute the complete value loop: launch → input → main action → result → save/complete → reopen/use result, adapted to the product. Do not mark Covered because controls exist or isolated steps launch.

## Negative / Failure

Remove ideal conditions: deny permission, make resources/network/data unavailable, trigger invalid state or operation/save failure, and test whether the user can understand and recover. An error modal alone does not prove recovery.

## Boundary

Exercise empty, zero, one, minimum, maximum, very small/large, long/no content, slider endpoints, and item-count limits that are relevant to the product.

## State Transition

Test sequences and return paths such as A → B → C → A. Combine modes, edit states, navigation, settings, input sources, and main actions; many failures occur between otherwise valid static states.

## Rapid / Repeated / Abuse

Use rapid, repeated, double, retry, modal open/close, fast navigation, repeated save/capture, control switching during processing, and actions before the previous operation finishes. Prefer automation for repeatable stress; do not assume normal users never do this.

## Race / Async

When asynchronous work exists, test duplicate requests, stale/late results, cancel/restart, repeated action during loading, back/dismiss during work, and close-together state changes. Use `ENGINEERING.md` ownership and lifecycle clues.

## Lifecycle

Consider foreground/background, lock/unlock, kill/relaunch, interruption, system settings round-trips, external permission changes, and other platform lifecycle transitions relevant to the product.

## Persistence / Recovery

Verify state after exit/reopen, unfinished-task handling, temporary resources, partial save, failed-task cleanup, state restoration, and generated-file lifecycle.

## Device / Adaptation

Test portrait, landscape, rotation during interaction, small/large screens, safe areas, supported device classes, keyboard, and split layout when relevant. Verify that functionality remains visible, reachable, operable, unclipped, and state-preserving; do not merely glance at rotation.

## Accessibility

Objectively test Dynamic Type, VoiceOver, labels, focus order, touch targets, text clipping, reachable important controls, and contrast only when measurable. Inoperability is a testing concern; visual taste is not.

## Hardware / Platform-specific

Map real environments for camera, microphone, GPS, Photos, Bluetooth, sensors, MultiCam, flash, Live Photo, hardware buttons, and platform services. Mark Simulator-inexpressible requirements with `Status: Blocked` or `Partial` as justified and disposition `Guided Physical Testing Required` or explicitly accepted `Deferred`; never infer device coverage from Simulator success. Phone mirroring is not a physical-device product-testing route. Device discovery, signed build, install, and launch are supporting capability evidence, not hardware-behavior coverage.

## Stress / Performance

Run lightweight risk-based stress such as continuous capture/export, long preview, rapid mode switching, many assets, repeated processing, and observation for memory growth, visible lag, freeze, or device thermal issues. Do not turn every Campaign into a full performance benchmark.

## Data Integrity

Verify saved output, deletion target, ordering, metadata, preview/output agreement, cancel cleanup, duplicate creation, and state after partial failure.

## Privacy / Destructive Behavior

Check least-required permissions, limited access modes, denied location/media, delete confirmation, overwrite behavior, accidental permanent deletion, and agreement between success UI and actual storage. Keep this product-focused; do not expand into a legal audit.
