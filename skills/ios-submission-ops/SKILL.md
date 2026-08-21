---
name: ios-submission-ops
description: Guide one Ready Final Candidate through Apple Developer and App Store Connect operations, Archive, Validate, Upload, Submit for Review, and verified Waiting for Review closeout. Use when a project is Ready for Submission Operations with a Final Candidate, Trusted Engineering Baseline, still-valid Testing evidence, and Release Readiness handoff; preserve upstream evidence, orient the user through a nine-step journey, and route Candidate-affecting changes back to the appropriate upstream Skill instead of repeating testing, code review, or release readiness.
---

# iOS Submission Ops

## Definition

Guide one Ready Final Candidate through Apple Developer and App Store Connect operations, Archive / Validate / Upload, and Submit for Review, while keeping the user oriented at every step.

User language:

> 这版 App 已经准备好了，现在带我把它真正送进 App Store 审核。

Own only Submission Operations:

- confirm submission identity, rights/provenance delta, privacy/support data, and store assets;
- establish Apple Developer identity and the App Store Connect App record;
- complete account/distribution declarations and store metadata;
- Archive, inspect, Validate, Upload, complete the live ASC record, and Submit for Review;
- verify Waiting for Review and close out the run;
- triage a rejection by cause before routing it.

Do not repeat Full Testing, Initial Code Review, Full Release Readiness, architecture review, performance research, product redesign, or feature development.

Read [submission-sop.md](references/submission-sop.md) before material work. Use the templates only after deriving runtime product facts; never write runtime values back into this reusable package.

## Entry Contract and Routing

Enter normally with:

```text
Ready for Submission Operations
+ Final Candidate
+ Trusted Engineering Baseline
+ still-valid Testing evidence
+ Release Readiness handoff
```

Submission Ops consumes the Final Candidate; it does not reshape or independently re-approve it.

Route instead of copying another Skill:

- missing, invalid, or materially stale Release Readiness → `$ios-release-readiness`;
- source, binary, dependency, or configuration change invalidating the Trusted Engineering Baseline → `$code-review` Change Review;
- change that may affect product behavior → `$testing` Delta Testing / Fix Verification;
- reopened product direction, scope, or core experience → `$ship-real-mvp`.

Consume the public handoff of each upstream Skill. Do not reproduce its internal workflow, campaign, review system, or tracker. Historical reports may contribute evidence, but the current interface is the Trusted Engineering Baseline, Testing handoff, Final Candidate, and Release Readiness handoff.

## Final Candidate Ownership Boundary

Classify every Submission finding before changing anything.

**Store-side / submission-only changes** may remain here: description, keywords, subtitle, Review Notes, Age Rating answers, App Privacy answers, pricing/availability, screenshots that do not change the binary, Support URL, Privacy Policy URL, and ASC settings.

**Candidate-affecting changes** invalidate the Final Candidate: source, `Info.plist`, Entitlements, Capabilities, Bundle ID in the binary, device family, packaged resources, binary App Icon, `PrivacyInfo.xcprivacy`, build settings, dependencies, or bundled media.

Never silently change the Candidate and continue as though it were unchanged. Use:

```text
Candidate-affecting finding
→ perform or prepare the smallest justified fix
→ Release Readiness refresh
→ Code Review Change Review if the engineering baseline changed
→ Testing Delta if behavior may have changed
→ new Final Candidate
→ resume the same logical Submission module
```

Do not restart at Step 1 after a refresh.

## Evidence Reuse First

Open every internal gate with:

```text
Do we already have trustworthy evidence for this,
and does it still apply to the current Final Candidate?
```

- applies → `REUSE`;
- partially applies → `REFRESH DELTA`;
- invalid or absent → smallest sufficient new work.

Prefer evidence from Release Readiness, Testing, Code Review, MVP, and user evidence. Bind inherited evidence to the current Candidate. Compare reusable assets by content digest such as SHA-256, not filename. Internal gate detail must not become a user-managed checklist.

## The Nine-Step User Journey

Keep these nine user-visible steps. Internal gates are not the User Journey.

```text
① App 已经准备好      明确当前要提交的 Final Candidate
② 上架身份            名称、Bundle ID、版本、Build、Team、设备范围
③ 版权与来源          实际发布内容的 rights / provenance evidence consistent
④ 隐私与权限          行为、Apple 声明、Privacy Policy、Support 信息一致
⑤ 商店视觉资产        Icon、截图与 App Preview 决策 ready
⑥ Apple 身份与商店记录 Explicit App ID 与 ASC App record 正式存在
⑦ 商店资料            商店页面、账户声明与审核资料 ready
⑧ 打包上传            Candidate → Archive → Inspect → Validate → Upload → Processing
⑨ 提交审核            Submit for Review → verified Waiting for Review
```

Use only these module states in user-facing progress: `Completed`, `Current`, `Waiting`, `Blocked`, `N/A`.

Show or refresh the overall nine-step map at:

- first entry into Submission;
- resuming an in-flight Submission;
- completion of a major Step;
- entry into a new Human Gate;
- a blocker that routes across Skills;
- Final Candidate invalidation;
- Upload completion;
- immediately before Submit for Review;
- Waiting for Review closeout.

Do not repeat the whole map for minor actions inside one module. On resume, show the map, name the earliest open module, and continue there.

## User Orientation Contract

At every point, make it possible to answer within five seconds:

1. Which Step am I in?
2. Which meaningful module is current?
3. Where is it?
4. What is complete and what remains?
5. Does the user need to act?
6. Where does completion lead next?

Never make the user infer progress from browser logs, terminal output, Apple errors, tool calls, silence, or internal Gate IDs. Less gate ceremony must never mean less feedback.

### Position before instruction

Before every external UI action—human-operated or agent-operated—state:

```text
Platform → Page → Module → Field / Button
```

Then state the action. Never say only “填 App Privacy”, “注册 App ID”, or “改 Team”.

When the user must act, provide as available:

- platform, current page, module, and field/button;
- a direct URL verified in the current UI or current first-party documentation;
- click path and exact values;
- fields that stay at their verified defaults;
- expected completion state;
- the next module.

Do not assert UI navigation from memory. For Xcode, Apple Developer, App Store Connect, a browser console, or a hosting provider, inspect the current live UI or current first-party documentation first. If the UI differs, relocate before instructing. Mark an unverified location as needing current verification; never invent it.

### One meaningful module at a time

Work on one natural module, not an entire Step and not one field per conversation turn. Related fields inside the current module may be completed together. Verify completion before advancing.

Default module start report:

```markdown
### 上架进度 X / 9

当前：<Step + Module>

位置：
<Platform> → <Page> → <Module>

目标：<module outcome>

已确认：<reused evidence / prepared values>

现在：<agent action>

需要你：无需操作 | one real human action

完成后：→ <next module>
```

Do not expose detailed engineering evidence unless blocked or asked.

### Human Action Card

When the user truly must act, use:

```markdown
### 需要你操作

上架进度：X / 9
当前模块：<module>

位置：
<Platform> → <Page> → <Module> → <Field/Button>

打开：<currently verified direct URL, when available>
点击：<exact click path>
填写 / 选择：<exact values and verified defaults>
为什么需要你：<2FA / legal / irreversible / permission / decision>
完成标志：<actual target state>
完成后：告诉我“好了”即可；Agent 重新验证并继续。
```

Do not ask the user to diagnose the technical state.

### Agent Browser Action Card

If the host can operate the current browser session, still show position and ownership before an important module:

```markdown
### 当前操作

上架进度：X / 9
位置：<Platform> → <Page> → <Module>
我会：<navigate / fill / save reversible draft / verify>
需要你：暂时不需要
```

Then navigate, fill, save only when reversible and authorized, re-read the target, and verify. Report the outcome and next module without narrating every click.

An API, browser, automation, or tool success response is not completion:

```text
act → re-read actual target state → confirm expected value/state → Completed
```

## Step and Module Guidance

### ① App 已经准备好

Bind the exact Final Candidate and inherited handoffs read-only. Confirm Version, Build, Bundle ID, source/package identity, Trusted Engineering Baseline, Testing freshness, and Release Readiness outcome. Do not re-run upstream work.

### ② 上架身份

Confirm Product/Display Name, `CFBundleName`, Bundle ID, Developer Team, Version, Build, minimum iOS, device family, orientation, development region/localizations, and first-release/update status.

A renamed product can retain the old target name in `CFBundleName`. Read the built `Info.plist`. `INFOPLIST_KEY_*` is an allowlist, not a general `Info.plist` channel; there is no working `INFOPLIST_KEY_CFBundleName`. Renaming `PRODUCT_NAME` changes the `.app` and executable and can break `TEST_HOST` / `BUNDLE_LOADER`, so it invalidates evidence. Catch it during identity freeze; if discovered only after Archive, assess whether deferral is safer than reopening the Candidate.

Bundle ID must come from current project fact, approved product identity, or explicit user confirmation when genuinely undecided. Never invent or impose a personal/studio prefix.

### ③ 版权与来源

Cover every shipping font, music/BGM, SFX, image, illustration, App Icon, video, template, third-party item, and bundled medium. Reuse matching verified digests; delta-audit new or changed assets. `UNKNOWN` blocks Archive until provenance is established or the asset is replaced. Say `版权与来源证据一致`, never claim legal compliance.

### ④ 隐私与权限

Derive Privacy Truth in order: production APIs → permissions → data handling → production SDKs → Required Reason APIs → purpose strings → privacy-manifest applicability → ASC App Privacy → Privacy Policy → in-app access → Support page.

`UNKNOWN` stays `UNKNOWN`. Distinguish device-local processing from Apple’s Data Collected definition. A missing `PrivacyInfo.xcprivacy` is not automatically a defect; verify current requirements. Generate public pages from product truth, not boilerplate.

Use the current product’s approved and maintainable public hosting when possible. Valid options include an existing public site, product website, Notion public page, or another suitable provider. Notion is a supported lightweight option, never a permanent default. Verify no-login access, stable URL, mobile readability, correct product content, and absence of internal evidence.

Keep in-app Privacy Policy access at the inherited default `REQUIRED`. Its live-check is a freshness check, not a new applicability debate: unchanged Apple rules → remain `REQUIRED`; only an explicit current rule change may alter it. If the App lacks this access, the required UI/code change invalidates the Final Candidate.

### ⑤ 商店视觉资产

Precheck product correctness before the ASC record, then confirm actual live slots after the record exists. Never hardcode screenshot sizes or device slots.

Inspect the marketing icon file for an alpha channel; fully opaque alpha still counts. After any pixel edit, revalidate dimensions, channel, actual changed bounding box, and surrounding pixels. Reuse screenshots only when still equivalent to the Final Candidate. Record App Preview as `YES`, `NO`, or `N/A` based on current needs.

### ⑥ Apple 身份与商店记录

Always separate the systems and modules:

```text
6A Apple Developer → Register Explicit App ID
6B App Store Connect → Create App Record
```

At execution time, verify the current direct URL and click path for each. If the target Bundle ID is unavailable in `App Store Connect → New App → Bundle ID`, return to `Apple Developer → Identifiers`; the matching Explicit App ID must exist first. Never select a stale ID to pass the form.

### ⑦ 商店资料

Use natural, live-UI-confirmed modules, for example:

```text
7A App Information
7B Age Rating
7C App Privacy
7D Pricing & Availability
7E Version Information
7F Review Information
7G Account / Agreements / Distribution, when relevant
```

This is user-journey grouping, not a permanent claim about ASC layout. Inspect the live record before naming pages, required fields, defaults, or blockers. Work on one module at a time.

Account declarations can inherit historical state. Read live DSA, agreements, tax/banking, storefront, and availability values rather than assuming blank. A previously shipped App is bounded precedent only when category, storefront, account state, and current rules actually match.

In Review Information, explicitly verify the `Sign-in required` state. For apps without accounts, do not leave a credential requirement enabled. State device/data preconditions in Review Notes when a clean review device would otherwise show an unusable empty state.

### ⑧ 打包上传

Use these modules:

```text
8A Candidate Binding
8B Archive
8C Inspect
8D Validate
8E Upload
8F ASC Processing
```

Inspect the actual Archive identity and package. An `.xcarchive` is not the shipped IPA: automatic signing commonly leaves the archive with Development signing and `get-task-allow = true`; exported App Store IPA evidence must show Distribution signing, `get-task-allow = false`, and an appropriate store provisioning profile. Do not misdiagnose the archive signature as missing distribution signing.

Prefer Release-only exclusion of debug/test fixtures over deleting files that inherited tests depend on. Inspect the Release product for fixture absence.

Validate before Upload, always. Validate is a distinct check; Upload is an external Apple mutation.

Before Upload, show this strong Human Gate and require the user to say `上传`:

```markdown
### 需要你确认：即将上传 Build

上架进度：8 / 9
当前 Candidate：<App Name> — Version <Version>, Build <Build>
已经确认：Final Candidate identity · Archive · Validate · Bundle ID · distribution evidence · relevant release evidence
接下来：Upload 到 App Store Connect。
影响：该 Build number 将进入 Apple 流程。
需要你：明确确认“上传”。
```

Never auto-Upload.

### ⑨ 提交审核

After the build is processed, inspect the live ASC record and clear only the Required items it actually shows. Before submission, refresh the overall map and require the final Human Gate:

```markdown
### 最终提交确认

上架进度：9 / 9
当前 Build：<App Name> — Version <Version>, Build <Build>
App Store Connect：当前实际 Required items 已清除。
审核资料：<summary>
Release Method：<value>
Distribution scope：<value>
Review Notes：<summary>
Sign-in required：<verified value>
接下来：Submit for Review
结果：成功后目标状态为 Waiting for Review。
需要你：明确确认“提交审核”。
```

Never auto-submit. After the action, re-read ASC. Only a real `Waiting for Review` or Apple’s current equivalent closes the run.

Close out with [submission-closeout.md](templates/submission-closeout.md). Report:

```markdown
### 已提交审核

状态：Waiting for Review
Version / Build：<Version> / <Build>
这次上架已经完成：①–⑨ 全部完成
接下来：等待 Apple 审核。
```

Rejected → read Apple’s response, triage by cause, then route metadata, privacy/hosting, ASC response, binary change, code fix, or new build. Approved/Live → Post-launch / Release Retrospective. Never mechanically restart Submission.

## Mutable Apple Rules and Verify Before Asserting

Never bake in changing Apple facts: Xcode/SDK minimums, Required Reason APIs, SDK privacy requirements, screenshot slots/sizes, Age Rating questions, export compliance, ASC required fields, Mac/Vision availability, DSA, country requirements, or agreements. At the relevant module, inspect current first-party Apple sources or live state and record source/check date. Without access, mark `CURRENT OFFICIAL VERIFICATION REQUIRED`.

Verify the installed Xcode before asserting where an action lives, whether a build setting exists, or what a fix changes. Rebuild and read values from the built product when relevant. Verify external state after every action. Correct stale assertions briefly and re-derive the recommendation.

## Human Gates and Autonomy

Continue autonomously with authorized, local, reversible work: inspect repo/Candidate, inherit evidence, hash assets, draft metadata and public-page content, prepare exact values, compare screenshots, inspect live form requirements, save reversible drafts when authorized, inspect Archives, and run allowed local validation.

Stop only for Apple login/2FA, legal/DSA/agreement declarations, unresolved rights, unresolved privacy truth, product identity decisions, Candidate-affecting decisions, credentials unavailable to the Agent, irreversible external mutation, Upload, Submit for Review, publish, or release. Do not add “continue?” gates to ordinary form modules.

Follow repository instructions. Preserve unrelated user work. Never push, publish, release, mutate Apple systems, Upload, or Submit without the authority required by the current run.

## Output Language and Package Hygiene

Follow the current conversation language; default to simple Chinese for Chinese users. Keep progress concise and user-facing. Do not expose internal Gate IDs or create a giant board, submission database, tracker system, or user-managed checklist.

Keep this package product-, account-, and user-agnostic. Use placeholders such as `<App Name>`, `<Bundle ID>`, `<Developer Team>`, `<Version>`, `<Build>`, `<SKU>`, `<Privacy Policy URL>`, `<Support URL>`, and `<Review Contact>`. Runtime project values belong only to the current run and must never be written back into Skill source, examples, metadata, templates, or packaged ZIP.
