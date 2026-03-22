purpose: conditional shaping artifact workflow, artifact directory guidance, multi-artifact automation; output: when and how to write PRDs, tech specs, related shaping artifacts, use subagents, and run code review; use when: Plan phase at lite or full level.

# Planning: Shaping Artifacts and Multi-Artifact Automation

This file extends the Plan phase with:
1. **Conditional shaping artifacts** — template selection by solution size and work type
2. **Best directory for shaping artifacts** — where to write artifacts
3. **Multi-artifact automation** — loop through many shaping artifacts with Implement + Code Review subagents

---

## When to write shaping artifacts

Select the lightest useful artifact for the Mode, Depth, and solution size.

| Situation | Recommended artifact |
|-----------|----------------------|
| Narrow Explore or small Patch | No doc or brief plan |
| Discussing a direction or clarifying intent | Brief plan or user story |
| Product-facing feature framing | User story or PRD |
| Technical design, migration, integration, refactor | Brief plan or Tech Spec |
| High-risk feature/build with both product and technical complexity | PRD + Tech Spec |
| Architectural or policy decision needs durable rationale | ADR / decision memo |

### Solution size heuristic

- **Micro:** < 5 tasks, single module, low risk, reversible
- **Condensed:** 5–15 tasks, 1–3 modules, moderate risk
- **Full:** 15+ tasks, multi-module, high risk, migrations, one-way doors

---

## PRD vs Tech Spec selection

| Work type | Use PRD | Use Tech Spec |
|-----------|---------|---------------|
| User-facing feature, UX, product logic | ✓ | — |
| Refactor, API design, infra, performance | — | ✓ |
| Both product and technical depth | ✓ + Tech Spec (full only) | ✓ |

**Rule of thumb:** Product-centric → PRD. Tech-centric → Tech Spec. Mixed, high-risk, or cross-functional work → both.

**Plan agent:** When filling a template, preserve the YAML-style structure. Do not convert `## tasks` into prose. Keep `id`, `description`, `files` as explicit keys so the Implement agent can parse them.

---

## Best directory for shaping artifacts

**Preferred (human-readable, version-controllable):**

```
{workspace_root}/artifacts/shaping/
```

Examples:
- `artifacts/shaping/20260302-prd-feature-auth.md`
- `artifacts/shaping/20260302-tech-spec-api-v2.md`
- `artifacts/shaping/20260302-prd-checkout-flow.md`
- `artifacts/shaping/20260302-adr-retry-policy.md`

**Fallback (session persistence):**

```
/ai-rpi-protocol/memory/plans/
```

Use workspace `artifacts/shaping/` when:
- The artifact is a deliverable to share or review
- The task produces a standalone shaping artifact
- The user or project expects plans under version control

Use workspace `plans/` when:
- The repo already uses `plans/` and switching would add unnecessary churn

Use `memory/plans/` when:
- No shareable artifact directory exists at workspace root and creating it is out of scope
- The plan is session-specific and not meant as a long-term artifact

**Recommendation before generation:** If a shaping artifact heavier than a brief plan would help, explain why and ask before generating it unless the user already requested it.

**Directory creation:** If `artifacts/shaping/` does not exist at workspace root, suggest creating it. Do not block — fall back to `memory/plans/` if the user prefers or the repo standard is still `plans/`.

---

## Multi-artifact automation

When the Plan phase produces **multiple independent work items** (e.g., 3 features, 4 refactors) that can be implemented and reviewed separately:

### Detection

- Research or Planning yields a **list of N distinct deliverables**, each with its own spec
- Each item has clear scope, tasks, and can be implemented without blocking the others
- N ≥ 2

### Automated workflow

1. **Split:** For each deliverable, produce a separate shaping artifact under `artifacts/shaping/`.
2. **Implement loop:** For each PRD/spec:
   - Spawn an **Implement subagent** with: spec + phase instructions + code context
   - Subagent implements that deliverable only
   - Main agent presents results per item
3. **Review loop:** After each implementation (or after all, per user preference):
   - Run **Code Review skill** (`skills/code-review.md`) — deterministic checks + specialist agents (Security, Conventions, Architecture, Test Quality, Patterns, Documentation)
   - Spawn specialist subagents in parallel from `agents/code-review/` for changed files
   - Aggregate findings per `code-review-output-template.md`
   - Main agent presents review to user
4. **Verify:** For each item, confirm:
   - [ ] Implementation matches spec
   - [ ] Tests pass
   - [ ] Code review findings addressed (or explicitly deferred)

### When to suggest (not force)

- Present: *"This plan breaks into N independent deliverables. I can implement each via a subagent and run a code review per implementation. I can also package the outcome as a PR description, handoff note, review package, validation summary, or another useful delivery artifact. Want to proceed that way, or implement together?"*
- If the user prefers a single pass, do not split. Respect user choice.

### Subagent prompts (for Implement)

```
Task: Implement the spec in artifacts/shaping/[filename].md.
Format: Spec uses YAML frontmatter + structured sections (see planning-prd-techspec-guidance "Agent consumption"). Parse ## tasks in order; each has id, description, files[]. Honor in_scope/out_scope.
Context: [Research findings, constraints, chosen approach]
Rules: Follow /ai-rpi-protocol/core/phases/implementation.md.
Scope: Only this spec — do not expand.
Return: Changed files, validation results, any blockers.
```

### Code review (multi-agent)

Use the **Code Review skill** (`/ai-rpi-protocol/skills/code-review.md`) on the changed files.

Rules:
- let the skill own the review workflow and specialist selection
- use `/ai-rpi-protocol/templates/restate-code-review-request.md` only when the review target is unclear
- use `/ai-rpi-protocol/templates/code-review-output-template.md` for the final aggregated review output

---

## Checklist before suggesting multi-PRD automation

- [ ] Plan yields N ≥ 2 independent deliverables
- [ ] Each has its own PRD or Tech Spec
- [ ] Implementations do not block each other
- [ ] User has not explicitly asked for a single implementation pass
- [ ] IDE supports subagents (mcp_task or equivalent)

---

## Agent consumption (machine-parseable format)

Templates use **YAML frontmatter** and **structured sections** so Cursor, Claude Code, and other agentic AIs can parse them without ambiguity.

### Structure

- **Frontmatter:** `---`-delimited YAML block at top. Extract: `type`, `size`, `id`, `date`.
- **Sections:** Lowercase `## section_name` headers with consistent key-value or list-of-objects format.
- **Tasks:** Ordered list. Each task has `id`, `description`, `files` (array). Implement agent executes in order.
- **Scope:** `in_scope` and `out_scope` as YAML-style arrays.
- **Risks:** List of objects with `id`, `description`, `mitigation` (and `blast_radius`, `likelihood`, `impact` for full).
- **Done when:** Checklist. Parse `- [ ]` items. Reserved items: `tests_pass`, `rollback_verified`, `monitoring_validated` indicate validation steps the Implement agent must run.

### Parsing instructions for Implement agent

1. Read the spec file.
2. Extract frontmatter (`type`, `size`, `id`).
3. Parse `## tasks` — execute each `id` in order; use `files` for scope; use `description` and `reasoning` for context.
4. Honor `in_scope` / `out_scope` — do not implement out-of-scope items.
5. Before declaring done, verify all `done_when` items.

### Template meta (HTML comments)

Each template has an HTML comment at top: `<!-- purpose: ... agent: Extract: ... -->`. Use for debugging; strip before versioning if desired.

---

## Template paths

| Template | Path |
|----------|------|
| PRD Micro | `/ai-rpi-protocol/templates/prd-template-micro.md` |
| PRD Condensed | `/ai-rpi-protocol/templates/prd-template-condensed.md` |
| PRD Full | `/ai-rpi-protocol/templates/prd-template-full.md` |
| Tech Spec Condensed | `/ai-rpi-protocol/templates/tech-spec-template-condensed.md` |
| Tech Spec Full | `/ai-rpi-protocol/templates/tech-spec-template-full.md` |
