# GapLab App Development Skills

GapLab App Development Skills 是一组面向 App 开发、可模块化且可独立使用的 Agent Skills。

## What / 是什么

本集合将实践中的 App 开发协作模式整理为可组合的 Skills。整体设计强调 modular、composable、risk-based，而不是一套 universal SOP：只有在某个 Skill 的能力与当前需求相关时，才独立调用它。

## Skills / 技能

### [`ship-real-mvp`](skills/ship-real-mvp/)

接管现有 App，并将其推进到最小可运行、以证据为基础的 MVP 闭环。

### [`adapt-ui-from-references`](skills/adapt-ui-from-references/)

分析视觉参考，校准一个高保真的核心界面，再以该基线扩展。

### [`code-review`](skills/code-review/)

验证工程风险、修复安全的问题，并建立或更新可信工程基线。

### [`testing`](skills/testing/)

执行 risk-driven 的真实 App 测试，并独立验证修复结果。

### [`ios-release-readiness`](skills/ios-release-readiness/)

在进入提交流程前，验证一个明确的 iOS Release Candidate。

### [`ios-submission-ops`](skills/ios-submission-ops/)

带领一个 Ready Final Candidate 完成 Apple 提交流程，并确认进入 Waiting for Review。

## Architecture / 架构

每个 Skill 都是独立、可维护的 bundle。项目可以只使用与自身需求相关的 bundle；不要求遵循统一 pipeline。

## 安装 / 使用

`skills/` 下的每个目录都是 Skill bundle。对于支持 Agent Skills 的 host，请使用该 host 提供的 import 或 installation mechanism 安装或导入对应目录。本仓库不假设所有平台共用同一个安装路径。

在 host 支持显式 Skill invocation 时，可以使用 `$ship-real-mvp`、`$adapt-ui-from-references`、`$code-review`、`$testing`、`$ios-release-readiness` 或 `$ios-submission-ops`。

示例：

- 使用 `$ship-real-mvp` 接管现有 App，并从当前真实状态继续工作。
- 使用 `$adapt-ui-from-references` 将视觉参考整理为一个经过校准的核心界面，再扩展 UI。
- 使用 `$code-review` 验证工程风险，并建立或更新可信工程基线。
- 使用 `$testing` 通过 risk-driven 的真实 App 覆盖发现产品 Bug，或独立验证修复。
- 使用 `$ios-release-readiness` 在提交流程前检查一个明确的 iOS Release Candidate。
- 使用 `$ios-submission-ops` 带领一个 Ready Final Candidate 完成提交流程，并确认进入 Waiting for Review。

## Status / 状态

本仓库当前包含六个公开 Skill bundle：

- `ship-real-mvp`
- `adapt-ui-from-references`
- `code-review`
- `testing`
- `ios-release-readiness`
- `ios-submission-ops`

这些 Skills 都可以作为独立 bundle 使用。不同 Skill 的验证深度有所不同；当前范围和限制请参阅各 Skill 文档及仓库历史。

## Limitations / 限制

- 不同 Skill 的验证深度有所不同。
- 本仓库发布的 Skills 不声称已在每种环境中经过生产验证。
- 部分可选 specialist route 可能缺少直接验证。
- 不同 host 对 Agent Skills 和显式 Skill invocation 的支持有所不同。

## License / 许可证

本仓库及其中包含的 Skill bundle 使用 MIT License。Copyright (c) 2026 GapLab。详见 [`LICENSE`](LICENSE)。

仓库和 Skill 的历史记录见 [`CHANGELOG.md`](CHANGELOG.md)。
