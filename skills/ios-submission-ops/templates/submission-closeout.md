# Template — Waiting for Review Closeout

Write only after re-reading App Store Connect and confirming `Waiting for Review` or Apple’s current equivalent. This closes Submission Operations; it does not wait for Approved or Rejected.

Keep real runtime values in the run artifact only. Never copy the completed closeout back into this reusable Skill package.

---

## <App Name> 上架提交收尾

**状态：** Waiting for Review  
**提交时间：** <Timestamp>

### 版本身份

```text
Final Candidate identity: <Source / Package Identity>
Version / Build: <Version> / <Build>
Bundle ID: <Bundle ID>
Developer Team: <Developer Team>
Apple Developer identity: <Explicit App ID Runtime Reference>
App Store Connect record: <ASC Runtime Reference>
```

### 打包与上传

```text
Archive: <Identity / Date / Result>
Archive inspection: <Result>
Distribution evidence: <Result>
Validate: <Result>
Upload: <Result>
Processed Build: <Version / Build / State>
```

### 九步结果

```text
① App 已经准备好: <Completed>
② 上架身份: <Completed / Notes>
③ 版权与来源: <rights / provenance evidence consistent / resolution>
④ 隐私与权限: <Privacy Truth / App Privacy / manifest applicability>
   Privacy Policy: <Privacy Policy URL>
   Support: <Support URL>
⑤ 商店视觉资产: <Icon / screenshots / live slots / App Preview>
⑥ Apple 身份与商店记录: <Explicit App ID / ASC record verified>
⑦ 商店资料: <required modules complete / account-distribution notes>
⑧ 打包上传: <Archive / Validate / Upload / Processing complete>
⑨ 提交审核: <Submit confirmation / verified Waiting for Review>
```

### 分发与审核决定

```text
Storefronts / regions: <Distribution Scope>
EU distribution: <Runtime Decision>
Mac availability: <Runtime Decision>
Vision availability: <Runtime Decision>
Release Method: <Release Method>
Sign-in required: <Verified Value>
Review Notes: <Runtime Summary>
Review Contact: <Review Contact>
```

### 继承与刷新过的证据

```text
Trusted Engineering Baseline: <Reference / Freshness>
Testing handoff: <Reference / Freshness>
Release Readiness handoff: <Reference / Freshness>
Reused verified assets: <Runtime References>
Refreshed deltas: <Runtime References / N/A>
```

### 下一步

```text
Rejected        → Review Response Triage, then route by cause
Approved / Live → Post-launch / Release Retrospective
```
