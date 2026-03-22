purpose: version history; output: notable changes; use when: checking releases or version.

# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## 1.1.0 - 2026-Mar-22

### Added
- Codex IDE adapter: [`adapters/ides/codex.md`](./adapters/ides/codex.md).
- New core system docs for adaptive governance: progressive loading, operational units, validation model, artifact ladder, deterministic guardrails, evaluation flywheel, persistent project context, setup lifecycle, role-based collaboration, canonical contract/adapters, and ultra-light protocol.
- Expanded specialist agents and templates for stronger multi-lens reviews and reviewer handoff.
- Public launch assets: reliability benchmark and launch kit updates.

### Changed
- Startup behavior is now mandatory for every new conversation across entry surfaces (`AGENTS.md`, `CLAUDE.md`, protocol entry files).
- Adaptive runtime was formalized around Mode (`Explore`, `Discuss`, `Review`, `Patch`, `Feature`, `Build`), Depth (`minimal`, `balanced`, `full`), and Persona.
- Skill matching and code review routing were hardened: explicit review/audit requests now route to the full `skills/code-review.md` workflow.
- Validation and packaging were tightened with confidence calibration, acceptance mapping, reviewer-focus outputs, and proportional delivery artifacts.
- Durable project context now loads `memory.md` and project-scoped `user-preferences.md` early when present.

### Removed
- Legacy experimental workspace from the repo, keeping only the backend plan document.

## 1.0.1 - 2025-Feb-28

### Added
- **Code review and project preferences:** Code review sessions load and apply project-scoped preferences so findings and advice stay aligned with the repo's durable guidance.
- **Abstract rules from code review fixes:** When addressing repeatable review issues or preferences (for example, preferring one pattern over another), the framework suggests capturing the reusable rule in project-scoped preferences so future code avoids the same drift.
- **Implementation follows project preferences:** Implementation explicitly loads and applies durable project-scoped preferences so generated code stays aligned with the repo's current guidance.
- Project info includes a durable preferences file you can edit and keep loading across phases and upgrades.
- When files change, the assistant runs lint, suggests project-info updates, and follows the code-generation checklist.
- When asking questions, the assistant uses a standard format: question, short explanation, and a recommendation.
- Code review gets dedicated templates and planning support.

### Changed
- `planning.md`: Code review section now aligns review advice with project-scoped preferences and suggests abstract reusable rules for pattern or preference issues.
- `implementation.md`: Added explicit project-preference loading during implementation and a post-fix prompt to suggest durable preference additions when completing code review fixes. Later revisions standardized this surface on `user-preferences.md`.
- Historical note (1.0.1 behavior): AGENTS.md asked whether to use AI RPI Protocol and which mode (lite/full). This was superseded in 1.1.0 by mandatory auto-detected startup.
- Historical note (1.0.1 behavior): protocol rules loaded only when the user accepted the protocol. This was superseded in 1.1.0 by always-on startup behavior.

### Credits
- External contribution: [#3](https://github.com/MiguelAxcar/ai-rpi-protocol/pull/3) by [@fabioasdias](https://github.com/fabioasdias) ("Fix typos and enhance clarity in README"), merged on 2026-02-27.

---

## [1.0.0] - 2025-february (initial release)

### Added
- Initial release of AI RPI Protocol Framework
