# GapLab App Development Skills

GapLab App Development Skills 是 GapLab 面向公开发布整理的一组模块化 App Development Skills 仓库。

## What / 是什么

本集合把真实 App 开发中形成并持续验证的协作模式整理为可组合的 Skills。目标不是建立一套 universal SOP，而是提供 modular、composable、risk-based 的能力：项目只在确有相关风险或需求时独立调用对应 Skill。

本仓库是 curated public release channel，不是本地工作目录的备份，也不是本地 Skill 的第二个 source of truth。正常方向是：

```text
Local Working Skills → Curated Public Skills → Stable Public Release
本地工作 Skill → 精选公开 Skill → 稳定公开发布
```

本地工作源需要先经过检查、验证、隐私/来源/依赖审计，再整理到这里。后续版本提升和正式 release 决策仍由 Human 控制。

## Architecture / 架构

每个 Skill 都保持独立、可维护、可单独调用。未来的 suite 只负责说明它们之间的关系，不建立强制性的 waterfall pipeline。概念上的关系可能包括：

```text
Idea / Requirement
        ↓
产品塑造与 MVP 交付
        ↓
参考图驱动的 UI 校准（仅在视觉参考重要时）
        ↓
实现与工程审查
        ↓
测试与修复验证
        ↓
Release Readiness
        ↓
Submission Operations（仅在明确需要时）
```

项目可以根据证据和风险进入、跳过或回到其中某些能力。Suite 负责组织关系，不要求每个项目执行全部阶段。

## Status / 状态

**GitHub 仓库已公开 · `ship-real-mvp` 仍为 Public Release Candidate**

GitHub repository 现已公开。`ship-real-mvp` 仍是基于一轮有边界真实 App direct pilot 的 Public Release Candidate，Human Packaging Review 已通过。没有任何 Skill 被声明为 Released v1.0；该能力不是 production-proven。后续版本提升、Tag、GitHub Release、package publication 及其他正式 release 操作仍由 Human 控制。

## 安装 / 使用

`skills/ship-real-mvp/` 是可分发的 Skill bundle。对于支持 Agent Skills 的 host，请使用该 host 提供的 Skill import 或 installation mechanism 安装或导入此目录。本仓库不假设所有平台共用同一个安装路径。

在 host 支持显式 Skill invocation 时，使用 `$ship-real-mvp` 调用。

示例：

- 使用 `$ship-real-mvp` 接管现有 App，并从当前真实状态继续工作。
- 使用 `$ship-real-mvp` 将 prototype 推进为最小可运行产品闭环。
- 使用 `$ship-real-mvp` 继续一个 runnable MVP，不重新开始已经有效的产品探索。

Testing、Code Review、Release Readiness 和 Submission Operations 都是 optional specialist integrations。只安装 `ship-real-mvp` 也可以使用核心能力。

## 当前限制

- 当前证据包含一轮有边界的真实 App direct pilot。
- 该能力不是 production-proven。
- 并非每一条 optional specialist route 都有 direct validation。
- 后续版本提升、Tag、GitHub Release 及其他正式 release 操作仍由 Human 控制。

## Scope and boundaries / 范围与边界

- 本地工作 Skill 继续以其本地 source of truth 为准。
- 本仓库只应包含经过整理、适合该公开渠道的内容。
- 本地文件存在、成功执行、benchmark 或已有公开仓库副本，都不能单独证明 production maturity 或 public release readiness。
- 私有项目名、凭据、个人数据、session ID、机器相关路径、第三方媒体和许可证不清晰的内容，在纳入前都需要审核。

## License / 许可证

本仓库以及已打包的 `ship-real-mvp` 候选使用 MIT License，package provenance 中记录 `Copyright (c) 2026 GapLab`。这是对当前 package 的 Human ownership decision；未来加入第三方内容时仍需重新审核。

当前状态和 release history 见 [`skills/ship-real-mvp/PROVENANCE.md`](skills/ship-real-mvp/PROVENANCE.md)、[`VERSION_MANIFEST.md`](VERSION_MANIFEST.md) 和 [`CHANGELOG.md`](CHANGELOG.md)。
