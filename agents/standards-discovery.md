purpose: discover project conventions and standards; output: discovered standards artifact; use when: Code Review (before Conventions), generate project-info, before implementing, or any task needing project context.

# Standards Discovery Agent

**Type:** General-purpose discovery agent
**Purpose:** Find and infer project conventions — no assumptions about file names or structure. Works on any project (any language, any framework). Reusable by Code Review, project-info generation, Planning, and future skills.

---

## Invocation

```
Task: Discover this project's conventions and standards.
Target: [workspace root or specific directories]
Output: Structured artifact (documented + inferred conventions).
Context: No prior knowledge. Search and infer.
```

---

## Discovery steps

### 1. Search for convention documents

Search for files that typically document project rules. Do NOT assume specific names — use patterns:

- **Pattern docs:** `*PATTERN*`, `*CONVENTION*`, `*STYLE*`, `*ARCHITECTURE*`, `*GUIDE*`
- **Contributing:** `CONTRIBUTING*`, `CONTRIBUTE*`
- **Project instructions:** `AGENTS.md`, `*INSTRUCTIONS*`, `.cursorrules`, `.cursor/rules/*`
- **README:** Read README for "Conventions", "Architecture", "Getting Started" sections

**Output:** List of found files with one-line summary of what each contains.

### 2. Check project-info (if protocol is used)

If a project-info directory exists (for example `/ai-rpi-protocol_project-info/`, `*_project-info/`, or `project-info/`):
- `standards.md` — coding standards
- `stack-patterns.md` — stack and pattern conventions
- `structure.md` — module layout
- `constraints.md` — non-negotiable rules

**Output:** Paths and key topics from each.

### 3. Infer from project structure

- **Package manager:** package.json, pyproject.toml, Cargo.toml, go.mod, etc.
- **Framework:** Dependencies reveal framework — note for convention inference
- **Directory layout:** Common patterns (src/, lib/, app/, modules/, packages/)
- **Config files:** Config that implies conventions (tsconfig, eslint, pytest.ini)

**Output:** Framework/language, key dirs, config-driven conventions.

### 4. Infer from existing code (sample)

Pick 2–3 representative files in the target area (or adjacent). Extract:
- Naming patterns (files, classes, functions)
- Module/import structure
- Where similar logic lives
- How errors/tests are structured

**Output:** Inferred conventions from code samples. Mark as "inferred" not "documented".

---

## Output format

```markdown
# Discovered Standards: [project/dir]

## Documented conventions
| Source | Path | Key topics |
|--------|------|------------|
| [type] | [path] | [topics] |

## Inferred conventions
- **Framework:** [if detectable]
- **Structure:** [dir patterns]
- **Naming:** [from samples]
- **Other:** [any inferred rules]

## Gaps
- [No convention doc found — will rely on inference]
- [Unclear on X — consumer should note uncertainty]
```

**Keep it brief.** Consumers (Conventions reviewer, project-info generator, etc.) will read actual files when needed. This is a map, not a full transcript.

---

## Rules

- **No assumptions** — Use whatever convention docs the project has. Don't expect any specific file name.
- **Any language** — Python, JS, Go, Rust, Java, etc. Adapt search patterns.
- **Mark confidence** — "documented in X" vs "inferred from Y"
- **Fail gracefully** — If nothing found, output "No convention docs found. Consumer will infer from adjacent code and framework norms."
- **Reusable** — Output is consumable by any caller (Code Review, project-info, Planning, future skills).
