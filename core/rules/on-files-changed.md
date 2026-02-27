purpose: trigger post-change checks whenever files get changed; output: lint run, project-info update check, repo checks; use when: after any turn where project files were created, modified, or deleted.

# On files changed

**Trigger:** Whenever files get changed — that is, after any turn in which you or the user created, modified, or deleted one or more project files (code, config, or other repo files).

When this trigger fires, run the checklist below. Do not present "done" without having done these steps (or explicitly saying what you could not do and what the user should run).

---

## Checklist (run in order)

### 1. Lint and repo checks

- **Run** the repo’s lint (and typecheck/build if applicable). Use the project’s usual commands (e.g. `npm run lint`, `pnpm lint`, `cargo clippy`, `ruff check`, etc.).
- If you cannot run them (no sandbox, no runner), **say so** and **propose the exact commands** for the user to run.
- Do not claim checks passed without having run them or without telling the user to run them.

### 2. Code generation rules

- Load and apply `/ai-rpi-protocol/core/rules/code-generation-rules.md`:
  - Linter check (blocker: fix or acknowledge and propose fix)
  - Pattern compliance (stack-patterns)
  - Constraint compliance (constraints)
  - **Project-info update check** (see below)
  - Test coverage check
  - Documentation check

### 3. Project-info update check

After implementation, check if project-info needs updating:

| Change type              | May need update      |
|---------------------------|----------------------|
| New pattern introduced    | `stack-patterns.md`  |
| New constraint discovered | `constraints.md`     |
| New domain term used      | `glossary.md`        |
| New integration added    | `integrations.md`    |
| Architecture changed      | `structure.md`       |
| New standard or tool      | `standards.md`       |

If an update is needed, propose it (e.g. "Project-info update suggested: … Should I add this? [yes/no]").

---

## Scope

- **Applies to:** Changes to project files (source, config, scripts). You can skip this trigger for edits only to protocol files (e.g. under `ai-rpi-protocol/` or `AGENTS.md`) or to project-info docs themselves, unless the user asks for the check.
- **Applies when:** You are in Implementation phase or you have just made edits that affect project behavior. For trivial edits (typos, comment-only), a shortened check (e.g. lint only) is acceptable; for non-trivial code changes, run the full checklist.

---

## Summary

When you change project files: **run lint (and typecheck/tests if applicable), apply code-generation-rules (including project-info update proposal), and report what ran and what failed or what the user should run.**
