# App Development Skills Repository

This repository is GapLab's curated public release channel for modular App Development Skills, derived from a separate local/private working source. Do not assume or create bidirectional synchronization with any private source, and never perform a blind directory sync or treat this repository as its mirror.

Before adding public content, audit privacy, secrets, personal or machine-specific paths, provenance, third-party assets, and licensing. Public README content must remain consistent in English and Chinese. Important public commits must be bilingual, traceable, and explain What changed and Why.

Do not raise a Skill's maturity claim without evidence. Keep Skills modular and independently invokable; do not merge them into one giant Skill or create a mandatory universal workflow.

## Component Publishing Convention

When publishing a Skill component:

1. Use the current active working source; ignore archived or disabled historical versions unless explicitly needed.
2. Use only the stable public Skill name in public-facing content; do not expose internal version suffixes or private working identities.
3. Curate the current source into `skills/<public-name>/`; never blindly mirror the private working directory.
4. Run lightweight checks for secrets, personal or machine-specific paths, private artifacts, bundled third-party assets, and license conflicts.
5. Validate that the public bundle is structurally complete and that referenced local files exist.
6. Update only the public documentation affected by the new component.
7. Treat additional provenance, maturity, evidence, or historical review as exception-driven, not mandatory.
8. If publication is explicitly authorized and clean-path checks pass, normal commit and push may continue without intermediate Human prompts.
9. When Human explicitly says “publish” for an existing public repository and clean-path checks pass, complete publication directly to `main`; use a PR or Draft PR only when Human requests review/PR flow or a real blocker requires review.
10. Tags, GitHub Releases, v1.0 promotion, unclear rights, credentials, destructive actions, or unresolved risk require a separate Human decision.
