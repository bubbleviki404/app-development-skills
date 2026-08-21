# App Store Submission SOP — Internal Gate Detail

Working detail for `ios-submission-ops`. Apply by applicability, not as a mandatory matrix. Internal gates remain Agent-owned; expose only the nine-step journey, current meaningful module, location, action owner, completion state, and next module.

## Contents

1. Operating rules
2. Gate 1 — Ready Final Candidate handoff
3. Gate 2 — Submission identity
4. Gate 3 — Rights and provenance
5. Gate 4 — Privacy and permissions
6. Gate 5 — Store visual assets
7. Gate 6 — Apple Developer identity and ASC record
8. Gate 7 — Store information and account declarations
9. Gate 8 — Archive, Validate, Upload
10. Gate 9 — ASC completion and submission
11. Waiting for Review and rejection routing

Anything marked **live-check** must be verified against current first-party Apple documentation, the installed Xcode, or the live Apple target at execution time. Never infer completion from a tool response; re-read the target state.

## 1. Operating Rules

### Evidence reuse decision

For every gate:

```text
trustworthy and current for this Final Candidate → REUSE
partly current                              → REFRESH DELTA
invalid or absent                          → smallest sufficient NEW WORK
blocked by unresolved fact                 → BLOCKED and route/ask
not applicable                             → N/A
```

Record evidence provenance internally, but do not make the user manage it. Bind file evidence by digest when identity matters.

### Candidate boundary

Store-side changes stay in Submission Ops. Any source, binary, package, dependency, entitlement, capability, `Info.plist`, App Icon, `PrivacyInfo.xcprivacy`, device-family, or build-setting change invalidates the Final Candidate.

After the smallest justified fix, refresh Release Readiness; request Code Review Change Review if the Trusted Engineering Baseline changed, and Testing Delta if behavior might change. Resume the current Submission module after a new Final Candidate exists.

### External UI action protocol

Before a user or Agent acts, verify and report:

```text
Platform → Page → Module → Field / Button
direct URL if currently verified
click path
exact values and verified defaults
expected completion state
next module
```

Inspect current live UI or first-party documentation before asserting page names, controls, or routes. Use one meaningful module at a time. After acting, re-read and verify the expected state.

## 2. Gate 1 — Ready Final Candidate Handoff

Consume the Release Readiness handoff read-only:

```text
Ready for Submission Operations outcome
Final Candidate identity
App version / build
Bundle ID / target / scheme / Release configuration
source identity and relevant dirty state
Archive or release package identity, if already present
Trusted Engineering Baseline and remaining engineering risk
still-valid Testing / user / physical-device evidence
release-specific checks and known nonblocking deferrals
approved assets, privacy/support facts, and submission intent
```

Confirm that all release-affecting state belongs to the Candidate and that unknown local work does not enter it. Never clean, stash, delete, or alter unrelated work.

If the handoff is absent, invalid, or materially stale, route to `$ios-release-readiness`. Do not reconstruct Full Readiness here.

User outcome: `① App 已经准备好` means one exact Final Candidate is identified and bound to still-valid upstream evidence.

## 3. Gate 2 — Submission Identity

Freeze exact runtime values without writing them into this reusable package:

```text
Product / Display Name (CFBundleDisplayName):
Short bundle name (CFBundleName, normally from PRODUCT_NAME):
Bundle ID:
Developer Team:
Marketing Version:
Build Number:
Minimum iOS:
Device family:
Orientation:
Development region (built CFBundleDevelopmentRegion):
Declared localizations (.lproj / CFBundleLocalizations):
First release / Update:
Canonical project source (generator | pbxproj | build settings):
```

### `CFBundleName` trap

A renamed product can retain the old target name in `CFBundleName`. `CFBundleDisplayName` is user-visible; `CFBundleName` also surfaces in crash logs and Apple tooling, including Organizer flows. Read both from the built `Info.plist`.

Xcode `INFOPLIST_KEY_*` settings are an allowlist, not a universal `Info.plist` escape hatch. `INFOPLIST_KEY_CFBundleDisplayName` and `INFOPLIST_KEY_ITSAppUsesNonExemptEncryption` may work in supported toolchains; `INFOPLIST_KEY_CFBundleName` does not provide a general fix. Verify installed Xcode behavior rather than relying on memory.

Changing `PRODUCT_NAME` moves the `.app` and executable and can break test targets through `TEST_HOST` / `BUNDLE_LOADER`. It is Candidate-affecting and can invalidate Testing and engineering evidence. Catch it at identity freeze. If discovered only at Archive, compare the real cost of reopening the Candidate with deferring it to the next tested version.

### Development region

The App Store language list can derive from the binary. When no `.lproj` bundles and no `CFBundleLocalizations` exist, it may fall back to `CFBundleDevelopmentRegion`. Read the built product, not only the project file. This differs from ASC Primary Language, which controls listing language. A correction is Candidate-affecting and needs rebuild and targeted verification.

### Project source and identity decisions

- Identify whether a generator file, `project.pbxproj`, or build settings are canonical before proposing a change.
- Regenerate only when objectively required; regeneration changes the Candidate.
- Derive Bundle ID from current project fact or approved product identity. If genuinely undecided, request explicit confirmation. Never invent a prefix.
- If a build already exists in ASC under the current Bundle ID, stop before changing it and request a product/release decision.
- Treat device family and orientation as product decisions, never warning-suppression choices.
- A Developer Team/signing correction is Candidate-affecting if it changes entitlements, capabilities, provisioning behavior relevant to runtime, packaged resources, or supported functionality.

## 4. Gate 3 — Rights and Provenance

Sweep every asset that actually ships in the App or store material:

```text
Fonts · Music/BGM · SFX · Images · Illustrations · App Icon
Bundled video · Templates · Third-party content · Other packaged media
```

Per asset, record internally:

```text
runtime path
content digest
matching verified evidence, if any
status: VERIFIED_REUSED | VERIFIED_NEW | UNKNOWN | REPLACED | N/A
evidence location
```

Rules:

- same filename or similar style does not prove identity;
- byte-identical verified assets may reuse their evidence;
- new or changed assets receive only a delta audit;
- `UNKNOWN` blocks Archive until ownership/license/provenance evidence is sufficient or the asset is replaced;
- do not provide legal advice or claim legal compliance; conclude only `rights / provenance evidence consistent` / `版权与来源证据一致`.

## 5. Gate 4 — Privacy and Permissions

Derive the truth in this order; never start from a generic Privacy Policy:

```text
production source
→ permission truth
→ data-handling truth
→ production third-party SDK inventory
→ Required Reason API audit
→ purpose strings
→ PrivacyInfo.xcprivacy applicability
→ ASC App Privacy truth table
→ public Privacy Policy
→ in-app access
→ public Support page
```

### Permission truth

For every production capability, determine actual API use, authorization request, required key, key presence, and wording consistency. Include as applicable Photos read/write, Camera, Microphone, Location, Contacts, Notifications, Tracking/ATT, Bluetooth, Files, Speech, Health, Calendar, and other protected APIs. A present but unused purpose key is a finding, not a pass.

### Data-handling truth

Establish from source and actual configuration:

```text
accounts/login · backend · content upload · analytics · crash reporting
ads · tracking · identifiers · diagnostics · usage data · payments
production third-party SDKs · network behavior · retention/deletion
```

Each answer is `YES`, `NO`, or `UNKNOWN` from evidence. Never turn product impression into `NO`.

### Current Apple privacy requirements

- inventory production SDKs and **live-check** current privacy-manifest requirements;
- **live-check** the Required Reason API list;
- conclude `PrivacyInfo.xcprivacy = required | N/A` from actual APIs and SDKs; never add a speculative manifest;
- derive ASC App Privacy from behavior, distinguishing device-local access/processing from Apple’s Data Collected definition;
- **live-check** the current ASC questionnaire.

### Public pages and in-app access

Draft [notion-privacy-policy.md](../templates/notion-privacy-policy.md) and [notion-support.md](../templates/notion-support.md) from confirmed truth only. Despite the filenames, the templates are provider-neutral and merely Notion-friendly.

Prefer the product’s existing approved, public, maintainable hosting. Other suitable providers, including a lightweight public Notion page, are valid when approved. Verify each page signed out, on mobile, and after publishing:

```text
public without login · stable public URL · readable on mobile
correct current product content · no private/internal release evidence
```

In-app access to the Privacy Policy keeps the inherited default `REQUIRED`. The current Apple-rules live-check is freshness verification only: unchanged rules → remain `REQUIRED`; only an explicit current rule change may alter it. Do not reopen applicability merely because the App has no account, server, or collected data. If a UI/code change is needed, invalidate the Final Candidate and route the refresh; do not make the change invisibly inside Submission.

## 6. Gate 5 — Store Visual Assets

Run in two passes because the live ASC record is authoritative for offered slots.

### 5A — Product-correct precheck before ASC record

App Icon:

```text
final approved product icon
correct asset catalog and target
no placeholder/dev/historical-product residue
present in the Release/Archive product
current Apple requirements satisfied (live-check)
```

Inspect the 1024 marketing icon file for an alpha channel; visible opacity is insufficient because an all-255 alpha channel still exists. This is a known Validate/upload failure surface. If a pixel edit is justified, detect the actual changed bounding box, verify surrounding pixels before painting, and revalidate dimensions, colors/channel, and the exported file afterwards.

Screenshots:

```text
existing export → compare with current Final Candidate UI
equivalent      → REUSE
materially changed → regenerate only affected screenshots
```

Confirm current product name, current UI/functions, localization, decided device family, current published format, and ordering. Record an explicit App Preview decision; optional does not mean forgotten.

Exit with product-correct candidate assets and a stated slot assumption, not a claim that ASC slots are satisfied.

### 5B — Live slot confirmation after ASC record

Open the live version page and read:

```text
device slots currently offered
required vs optional slots
record localizations
accepted dimensions / format
```

Reconcile the 5A set. Generate only proven gaps, remove obsolete assumptions, upload when authorized, then re-read ASC to confirm acceptance. Never hardcode device sizes or slot layouts in the Skill.

## 7. Gate 6 — Apple Developer Identity and ASC Record

Treat these as two different systems and meaningful modules:

```text
6A Apple Developer → Certificates, Identifiers & Profiles → Identifiers
   → register Explicit App ID

6B App Store Connect → My Apps
   → create App Record
```

At runtime, inspect current UI/first-party documentation and verify the direct URL, page names, click path, fields, and defaults before presenting a Human Action Card.

### 6A Apple Developer

Prepare exact runtime values:

```text
Description: <App Name>
Bundle ID: <Bundle ID> (Explicit; exact binary match)
Capabilities: only those the current product actually requires
Team/signing context: <Developer Team>
```

Human handles login/2FA, permission-controlled creation, and final confirmation. Re-read the Identifiers list and confirm the target Bundle ID before marking complete.

### 6B App Store Connect

Prepare exact runtime values based on the live form:

```text
Platform
App Name
Primary Language
Bundle ID
SKU
User Access
```

If `<Bundle ID>` is absent from the Bundle ID selector, report the current location and return to 6A; never choose a stale identifier. After creation, re-read the App record identity before marking complete.

## 8. Gate 7 — Store Information and Account Declarations

Do not present Gate 7 as one large form. Confirm the live ASC layout and group it into current natural modules, one at a time. A typical—not permanent—journey is:

```text
7A App Information
7B Age Rating
7C App Privacy
7D Pricing & Availability
7E Version Information
7F Review Information
7G Account / Agreements / Distribution, if relevant
```

For each module, report position, exact fields/values/defaults, owner, expected saved state, and next module. Agent may fill reversible authorized drafts; human retains legal, irreversible, permission-limited, or subjective decisions. Re-read after saving.

### Account and distribution truth

Account-level declarations are inherited, not blank. Read the live state for:

```text
agreements and actual blockers
Paid Apps Agreement applicability to the current business model
tax/banking applicability
DSA trader state and current distribution interaction
storefronts/regions and EU distribution
Mac “Designed for iPhone” availability
Vision availability
country/category-specific requirements only when relevant
```

Do not make false declarations to avoid public contact requirements. If the user rejects a required disclosure, adjust distribution scope only through an explicit truthful decision.

A previously shipped App under the account is bounded precedent, not universal proof. Reuse it only when category, storefront, business model, account state, and current rules match; identify the unmatched boundary.

### Metadata and review information

Confirm live required/optional status for App Name, Subtitle, Description, Keywords, Promotional Text, Marketing URL, Privacy Policy URL, Support URL, Category, Copyright, Age Rating, Content Rights, Pricing, Availability, Review Contact, Review Notes, sign-in requirement, and Release Method.

Release Method controls post-approval release behavior, not review speed.

Two real review traps:

- **Sign-in required** can inherit or default to an incorrect enabled state. Verify it explicitly; an App with no account system must not imply review credentials exist.
- **Review device/data preconditions** must be stated. If the core flow needs existing photos, a prior recording, an imported file, or other device state, explain this in Review Notes so a clean review device does not stall on an empty screen.

## 9. Gate 8 — Archive, Validate, Upload

Use user-facing modules:

```text
8A Candidate Binding
8B Archive
8C Inspect
8D Validate
8E Upload
8F ASC Processing
```

### Candidate binding

Reconfirm the exact unchanged Final Candidate and all current evidence. If any Candidate-affecting fix occurred, require the refreshed upstream handoff and new Candidate before continuing.

### Archive and inspection

Archive for the current physical-device distribution destination, not a Simulator. Do not hardcode Xcode UI wording; inspect the installed Xcode first.

Inspect at least:

```text
App/display name · CFBundleName · Bundle ID · Version · Build
signing · entitlements · capabilities · built Info.plist
privacy manifest when applicable · App Icon · shipping resources
absence of debug/test residue · absence of internal/local paths
```

For test fixtures bundled for tests, prefer Release-only exclusion such as `EXCLUDED_SOURCE_FILE_NAMES` over deleting the fixtures. Deletion can invalidate inherited tests without improving the shipping product. Confirm absence in the Release package.

### Archive is not the shipped IPA

Under automatic signing, the `.xcarchive` can correctly contain Development signing and `get-task-allow = true`. Distribution signing is applied during App Store export. Inspect the exported IPA when proving distribution:

```text
.xcarchive → development signing may be normal
exported IPA → Apple Distribution
             → get-task-allow = false
             → appropriate store provisioning profile
```

Do not infer a missing distribution certificate from the archive signature alone. Exporting is also useful proof that distribution signing is available.

### Validate before Upload

Run Validate as a distinct action before Upload. A failed validation does not enter a Build into ASC; Upload does. Re-read the validation result and classify the real cause. Diagnose signing/certificate failures minimally rather than preemptively hand-managing certificates.

Upload is a strong Human Gate. Show Candidate, Version, Build, identity, Archive/Validate, distribution evidence, impact, and exact confirmation word. Do not upload until the user explicitly confirms `上传`. After Upload, re-read ASC processing state and refresh the overall progress map.

## 10. Gate 9 — ASC Completion and Submission

Only after processing completes, inspect the live record and clear the items it currently marks Required, including as applicable:

```text
processed Build selection · screenshots · metadata · App Privacy
Age Rating · Content Rights · Export Compliance · Review information
availability · pricing · release method · account/compliance blockers
```

Never claim completeness from a remembered list. Re-read the current live record.

Before Submit for Review, refresh the nine-step map and present the final Human Gate with current Build, actual required-item state, review materials, Release Method, distribution scope, Review Notes, and verified sign-in requirement. Do not submit until the user explicitly confirms `提交审核`.

After the action, re-read ASC. A click or automation success is not submission success.

## 11. Waiting for Review and Rejection Routing

Only a real `Waiting for Review` or Apple’s current equivalent permits [submission-closeout.md](../templates/submission-closeout.md). Close Submission Ops then; do not wait for approval.

If rejected, read Apple’s actual response and referenced guideline, then route by cause:

```text
metadata/screenshots wording      → current Gate 7 / Gate 5 module
privacy disclosure mismatch      → Gate 4 truth + ASC App Privacy
privacy/support hosting problem  → Gate 4 public pages
missing review/demo information  → Gate 7 Review Information / ASC response
binary/config/package change     → Candidate invalidation + Readiness refresh
source/dependency change         → Code Review Change Review + Readiness refresh
behavior-affecting fix           → Testing Delta + Readiness refresh
product/guideline interpretation → product decision via $ship-real-mvp
new binary required              → new Final Candidate + resume at Gate 8
```

Never rerun the whole submission because one item was rejected.
