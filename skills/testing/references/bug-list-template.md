# Unified Bug List Template

Render every user-facing heading, field label, and explanation in the user's current conversation language. If the session is in Chinese, translate the English scaffold below and write `BUG-LIST.md` in Chinese. Keep code, commands, paths, model names, and original errors in their source language when useful.

Include confirmed, objectively demonstrable behavioral bugs only. Keep suspected findings and Expert Review Signals in the Testing Report. Use one entry per distinct user-visible problem and link only evidence that exists.

```markdown
# Unified Bug List — <Product / Build>

Source report: `<relative path to TESTING-REPORT.md>`
Campaign: `<Campaign ID / objective or N/A>`
Session: `<Session ID>`

## Summary

| Severity | Count |
|---|---:|
| Critical | 0 |
| High | 0 |
| Medium | 0 |
| Low | 0 |

## <BUG-ID> — <Concise user-visible title>

- Severity: <Critical / High / Medium / Low>
- Confidence: <High / Medium / Low>
- User goal: <what the user was trying to accomplish>
- Environment: <device, OS, state when known>
- Tested source: <HEAD, or HEAD + current working tree; link the source identity in the report>
- Tested build / artifact: <build ID, path, or hash when known>
- Preconditions: <minimum known starting state>
- Reproduction: <successful reproductions>/<attempts>
- Verification status: <Not yet verified / Fixed / Reopened / Still Blocked / Needs Verification>

### Steps

1. <action>
2. <action>
3. <action>

### Expected

<Reasonable product behavior; identify an assumption if no source defines it.>

### Actual

<Observed behavior without root-cause speculation.>

### User impact

<Reach, consequence, recoverability, and any data/safety impact.>

### Evidence

- `<screenshot/video/log/hierarchy path or artifact URI>` — <what it proves and retention status>
- `<flow path>` — isolation: <Isolated / Not fully isolated>; permission state: <...>; app state: <...>; data state: <...>; fresh launch: <Yes / No>; existing project/media dependency: <...>; rerun: `<exact invocation>`

### Builder handoff

<Any bounded implementation context the Builder needs. Do not prescribe an unverified root cause or fix.>

### Fix verification

<After Builder implementation, record changed build/source, original reproduction rerun, targeted variants, affected-surface regression, adjacent Campaign regression, evidence, and the Testing-owned verification status. Until then, keep `Not yet verified`; Builder completion means Implemented, not Fixed.>
```

When there are no confirmed bugs, write:

```markdown
# Unified Bug List — <Product / Build>

Source report: `<relative path to TESTING-REPORT.md>`
Campaign: `<Campaign ID / objective or N/A>`
Session: `<Session ID>`

No confirmed bugs in the executed coverage. This is not a claim that the product has no bugs; see the report for actual and missing coverage.
```

When `Testing Status: Environment Blocked` and Active Testing is `0 min`, do not use the generic no-bug wording above. Write a localized blocked result instead. In Chinese include exactly:

```markdown
Testing Status: Environment Blocked

本轮尚未实际测试产品 UI。环境恢复期间没有执行主动产品测试，因此不能据此判断产品是否存在 Bug。阻塞详情与 Resume State 见 `TESTING-REPORT.md`。
```

Severity guide:

- `Critical`: safety, severe data loss, security, or the primary product is unusable with no practical recovery.
- `High`: core flow is blocked or materially wrong for affected users; recovery is absent or costly.
- `Medium`: meaningful degradation with a workaround or limited reach.
- `Low`: minor but real usability, visual, or accessibility defect with limited impact.

Do not use `Low` to admit pure visual preference, subjective quality judgment, product-scope disagreement, or unsupported UX opinion. Route those observations to `Expert Review Signals` in the Testing Report.
