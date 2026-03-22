purpose: generate tests that match the project's existing style; output: test files + validation; use when: user asks to add, generate, or write tests.

# Skill: Automated Tests

Generate tests that match the project's house style. Study first, confirm scope, implement surgically.

---

## Phase 1: Scope — confirm with user

Before anything else, clarify what to test.

### Detect the change set

1. Identify the current branch: `git branch --show-current`
2. Identify the base branch (main, master, develop — check which exists)
3. Show the diff summary: files changed, lines added/removed
4. Present to the user: "You're on branch `<branch>`. Here's what changed vs `<base>`:
   - `<file>`: <summary of change>
   - `<file>`: <summary of change>"

### Confirm scope

Ask the user:
- **What to test**: "Do you want tests for all changes, or specific files/features?"
- **Test types**: Based on what the codebase supports (see Phase 2), ask: "The codebase has [unit tests / integration tests / e2e tests]. Which do you want? Unit, e2e, both, all?"
- **Depth**: "Do you want comprehensive coverage or just the critical paths?"

Do NOT proceed until scope is confirmed.

---

## Phase 2: Study — learn the codebase's test style (MANDATORY)

Do NOT write any tests until you complete this research. The goal is to produce tests that look like they were written by the same team.

### 2.1 Test infrastructure

Read and understand:
- **Test config**: Jest config, pytest.ini, vitest.config, .mocharc, or equivalent. Understand the runner, setup files, and conventions.
- **Test directories**: Where do tests live? Next to source (`*.spec.ts`)? In a `test/` directory? Both?
- **Setup/teardown**: Global setup, test helpers, fixtures, factories. What already exists?
- **CI integration**: How are tests run in CI? Any special commands or flags?

### 2.2 Golden examples — find the style to mirror

Find 2-4 recent, well-written test files that are closest to the code being tested. These are your "goldens" — the style you must match exactly.

For each golden, extract:
- **File structure**: imports, setup, teardown, describe/it nesting
- **Naming conventions**: test descriptions, file naming (`*.spec.ts`, `*.test.py`, `*_test.go`)
- **Setup patterns**: factories, fixtures, builders, mocks, DI bootstrapping
- **Assertion style**: which assertion library, patterns, level of specificity
- **Comment style**: verbose or sparse? Labels or explanations?
- **Mocking patterns**: what gets mocked, how, what gets spied on
- **Cleanup patterns**: how is state cleaned up between tests?

When conventions are still unclear, run `/ai-rpi-protocol/agents/standards-discovery.md` first and use its output to guide naming, structure, and helper reuse decisions.

### 2.3 Helpers and factories to reuse

Inventory existing test utilities:
- Factories (data builders, fixtures)
- Helpers (login, setup, request builders)
- Shared mocks or stubs

Rule: **reuse** existing factories and helpers. Do NOT create new ones unless no equivalent exists.

### 2.4 Existing coverage

For each file/class/function in the change set:
- Check if tests already exist
- Check what's covered (happy path only? edge cases? error paths?)
- Check the depth — does the team write minimal tests or thorough tests?

Present findings to user: "Here's what I found about the test infrastructure and current coverage. Here's what I suggest we add."

---

## Phase 3: Propose — relevance-gated test plan

For EACH candidate test, apply a relevance gate before writing it.

### Relevance check

- If similar code in the repo is **happy-path only**, keep the same depth. Do NOT add edge cases the team doesn't write.
- Add edge/error cases only when:
  1. The implementation introduces a new branch/guard not covered elsewhere, OR
  2. There's a regression risk with no equivalent test in the suite
- If a test would be redundant with existing coverage, **skip it**.

### Propose format

Present a checklist to the user:

```
Proposed tests:

1. KEEP — [test description] — [one-line justification citing exemplar]
2. KEEP — [test description] — [justification]
3. SKIP — [test description] — [why redundant, citing existing test]
```

Wait for user approval before implementing. User may add, remove, or modify.

---

## Phase 4: Implement — mirror the goldens

### Rules

- **Mirror the nearest golden** for structure, naming, setup, assertions, and comments.
- **Surgical edits only** — do not touch production code, configs, or unrelated helpers unless strictly required.
- **Reuse existing factories and helpers** — do not invent new ones unless no equivalent exists.
- **Match comment style** — if the codebase uses sparse label comments (e.g., `// pending state`), do the same. If it uses descriptive comments, match that. Do NOT impose a style the codebase doesn't use.
- **One test at a time** — implement, run, verify, then move to the next.

### Per-test workflow

1. Implement the test using the nearest golden pattern
2. Run the test (unit command or targeted test file)
3. If it fails, fix it
4. Verify comment style matches the codebase
5. Move to next test

### What to run

Identify the correct test commands from:
- `package.json` scripts (npm/yarn/pnpm)
- `Makefile` / `Taskfile` / `justfile` targets
- `pyproject.toml` / `pytest.ini` / `tox.ini`
- `go test` conventions
- CI config files
- Docker/docker-compose test commands (e.g., `kool run`, `docker compose exec`)

If you can't determine the command, ask the user.

---

## Phase 5: Report

Present results to the user:

```
Tests added:
- <file>: <what it tests>
- <file>: <what it tests>

Coverage:
- Happy path: [list]
- Error/edge: [list]
- Skipped: [list with reasons]

Validation:
- Tests run: <command>
- Result: <pass/fail>
- Build: <pass/fail if applicable>

Patterns followed:
- Mirrored: <golden file(s)>
- Reused: <factories/helpers>
- New utilities created: <none, or list with justification>
```

Before finalizing report on non-trivial test changes, optionally run:
- `/ai-rpi-protocol/agents/code-review/test-quality-reviewer.md` for false-confidence and coverage-depth issues
- `/ai-rpi-protocol/agents/code-review/patterns-reviewer.md` when test naming/style consistency is a concern

---

## Guardrails

- **Study first, write second.** Never generate tests without studying the existing style.
- **Do not refactor production code.** Tests only. If you find a bug during testing, report it — do not fix it unless the user asks.
- **Prefer recent exemplars** over legacy tests. Test patterns evolve; use the newest.
- **No flaky tests.** No global state leaks, no timing dependencies, no non-deterministic assertions.
- **No test bloat.** Add only tests that provide meaningful signal. If the team writes lean tests, write lean tests.
- **Respect the team's depth.** If the codebase is happy-path-only, do not suddenly add exhaustive edge case coverage unless the user explicitly wants it.
