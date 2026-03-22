purpose: strongest code review workflow with multi-agent specialist review; output: aggregated findings with options per issue; use when: user asks to review, audit, or examine code.

# Skill: Code Review

This is AI-RPI's default code review workflow. Any explicit request to review, audit, or examine code should route here. Review in a **fresh context** when that prevents confirmation bias and adds signal.

## References used
- Agentic Coding — Review in fresh context; iterative review
- AI Patterns (bdfinst) — Phase 1 (mechanical) vs Phase 2 (context-aware agents); specialist agents
- RKoots / IBM — Security, Architecture, Domain; adversarial validation
- Google eng-practices — Design, Functionality, Tests, Naming, Documentation
- Augment / Multitudes — Nine pillars; effectiveness at < 400 LOC

---

## Phase 1: Scope the review

If the review target is ambiguous, use `/ai-rpi-protocol/templates/restate-code-review-request.md`.

1. **Clarify scope only when needed**: if it is already obvious what code should be reviewed, skip the restate and move straight to scoping the review
2. **Identify the comparison surface:** staged changes, branch diff, selected files, commit range, or PR
3. **Prepare the diff view** when reviewing branch work against a base branch:
   ```bash
   # Target branch: $ARGUMENTS or main
   git diff <target>...HEAD --stat
   git log <target>..HEAD --oneline
   git diff <target>...HEAD   # full diff for agents
   ```
4. **Size the reviewable unit:** if the change is broad enough that one pass will become shallow, recommend splitting or reviewing in slices
5. **Confirm the scope** before proceeding when there was any real ambiguity or a meaningful review-scope choice

**Gate:** User confirms scope and focus. Do not proceed without confirmation.

---

## Phase 2: Run the cheap certainty checks first

Before invoking specialists, run the fastest reliable checks that can immediately invalidate the review surface. There is little value in deep review on code that already fails obvious project checks.

1. **Build / compile** — does it build?
2. **Lint** — run project linter (eslint, ruff, go vet, etc.)
3. **Format** — run formatter (prettier, black, gofmt)
4. **Tests** — run existing test suite
5. **Security scan** — if available (npm audit, pip-audit, snyk, etc.)

**If any fail:** Report and stop. Fix or escalate before specialist review.

**If all pass:** Proceed to Phase 3.

---

## Phase 3: Load intent and choose the review shape

When conventions are still unclear, run **Standards Discovery** (`/ai-rpi-protocol/agents/standards-discovery.md`) first. It searches for project convention docs and infers standards from code. Pass that artifact only to review lenses that need it.

```
Task: Discover this project's conventions and standards.
Target: [workspace or directory being reviewed]
Output: Structured artifact with documented + inferred conventions.
```

When `/ai-rpi-protocol_project-info/constraints.md` exists:
- always load it before spawning specialist agents
- extract the constraints that materially affect the review
- pass the relevant constraints to every specialist agent, not only Security

Reason:
- compliance, privacy, and regulated-system constraints cut across security, architecture, and correctness review

When the diff includes dependency upgrades, new third-party integrations, or uncertainty about external behavior:
- run `/ai-rpi-protocol/agents/documentation-researcher.md` (and `/ai-rpi-protocol/agents/web-researcher.md` when current advisories/release behavior matter) before finalizing security/performance conclusions
- pass validated external facts to specialist reviewers instead of relying on memory alone

When reviewing a branch or PR diff:
- check whether the diff includes planning or shaping artifacts such as `plans/*.md`, `artifacts/shaping/*.md`, tech specs, PRDs, ADRs, rollout notes, or equivalent intent-setting docs
- if found, load the relevant artifact and include it in review context

Use the shaping artifact to:
- understand what was intended, not just what was changed
- flag deviations from the planned design, rollout, or validation expectations
- distinguish intentional scope cuts from likely oversights

Pick the review shape before spawning specialists:
- **Direct multi-agent review**: small, cohesive changes can be sent straight to the selected specialist agents without a survey pass
- **Partitioned multi-agent review**: broader changes should be mapped into coherent review slices first
- **Split warning**: if unrelated concerns are bundled together, say so explicitly

For direct multi-agent review:
- send the full review scope directly to the specialist agents
- skip the survey pass only because the scope is already small enough, not because the main thread should do the review itself

For partitioned multi-agent review:
- use `/ai-rpi-protocol/agents/codebase-mapper.md` first to build a review map
- the review map should identify:
  - coherent change slices
  - likely risk hotspots
  - dependencies between slices
  - cross-cutting concerns that multiple reviewers must keep in mind
- then run specialist reviewers against each slice with the full local context they need

Rule:
- the mapper creates the review map; it does not issue quality findings itself
- the main agent orchestrates and aggregates; it does not perform the substantive code review itself
- do not downgrade to a small verification path when the user asked for code review

---

## Phase 4: Run the right review lenses

The Code Review skill is a multi-agent review workflow. Specialist subagents are the default execution path, not an optional extra. A code review should run the full review workflow, not a reduced verification shortcut. Each should work in a fresh context and return structured findings.

### Core review lenses

| Agent | File | Focus |
|-------|------|-------|
| Code Review | `/ai-rpi-protocol/agents/code-reviewer.md` | Correctness, maintainability, clarity, reviewer readiness |
| Architecture | `/ai-rpi-protocol/agents/code-review/architecture-reviewer.md` | Design, boundaries, patterns, coupling |
| Performance | `/ai-rpi-protocol/agents/performance-reviewer.md` | Efficiency, scale implications, hot paths |
| Security | `/ai-rpi-protocol/agents/code-review/security-reviewer.md` | Auth, supply chain, binaries, build tampering |
| Packaging | `/ai-rpi-protocol/agents/packaging-reviewer.md` | Reviewer guidance, handoff quality |
| Challenger | `/ai-rpi-protocol/agents/challenger.md` | Hidden trade-offs, weak assumptions, false certainty |

Additional specialist reviewers still available when they add signal:
- `/ai-rpi-protocol/agents/code-review/conventions-reviewer.md`
- `/ai-rpi-protocol/agents/code-review/test-quality-reviewer.md`
- `/ai-rpi-protocol/agents/code-review/patterns-reviewer.md`
- `/ai-rpi-protocol/agents/code-review/documentation-reviewer.md`

### Allocation guidance

- Default standalone code review to the full core lens set:
  - Code Review
  - Security
  - Architecture
  - Performance
  - Packaging
  - Challenger
- Default to the strongest review posture even for small diffs; small scope only changes whether a survey pass is needed
- Add more lenses based on the change shape and risk
- Add Architecture when boundaries, wiring, layering, or rollout shape matter
- Add Security for exposed surfaces, dependencies, external integrations, or governed data
- Add Packaging when the main challenge is reviewer handoff quality
- Add Performance when the change touches throughput, latency, caching, or scale-sensitive behavior
- Add Challenger when the implementation looks plausible but the assumptions still feel under-tested
- Add Conventions or Patterns when drift from established repo practice is a likely risk
- Add Test Quality when confidence depends heavily on the tests in the diff
- If the user narrowed the review focus, respect that unless doing so would hide a serious risk

Rule:
- small review does not mean main-thread review
- small review means skip the survey pass, not skip the specialist agents
- never replace this workflow with a lightweight verification pass when the request is code review

### Invocation shape

For each agent, spawn with:
```
Task: Code review from [agent] perspective.
Target: [files / diff summary]
Discovered standards (Conventions only): [artifact from Standards Discovery]
Relevant constraints: [/ai-rpi-protocol_project-info/constraints.md content or extracted regulatory / privacy / residency / operational constraints]
Focus: [agent-specific — see agent file]
Return: Structured findings per code-review-output-template format.
Context: Fresh — you did NOT write this code. Analyze objectively.
```

Rules:
- Agents run in separate contexts (no shared conversation with implementation)
- Each agent returns findings in the standard format (per-issue with severity, options, suggested approach)
- Main agent does NOT do the review — it orchestrates and aggregates
- When fields are created, transformed, validated, persisted, or exposed, reviewers should inspect the closest authoritative field definitions in models, schemas, migrations, database definitions, DTOs, contracts, serializers, or equivalent codebase sources before judging validation or format behavior

### Repository pattern fit

Pattern fit is a first-class review concern, not a cosmetic afterthought.

Check whether the diff introduces a new way of doing something where the repo already has an established approach:
- structural organization
- naming and file conventions
- error-handling patterns
- data-access patterns
- test placement and test shape
- frontend or client conventions when relevant

How to run it:
- For direct multi-agent review, pass a few analogous files or references to the relevant reviewer
- For partitioned multi-agent review, delegate to `/ai-rpi-protocol/agents/code-review/conventions-reviewer.md` or `/ai-rpi-protocol/agents/code-review/patterns-reviewer.md` with references to nearby code and discovered standards

Rule:
- deliberate pattern evolution is allowed, but it should be surfaced explicitly rather than arriving as accidental drift

---

## Phase 5: Merge findings into one review

1. **Collect** all specialist findings
2. **Collapse duplicates** while preserving useful multi-angle reasoning
3. **Rank by severity first** — highest severity first, then highest confidence within the same severity
4. **Resolve tension** — when specialists disagree, keep the disagreement visible and anchor it in evidence
5. **Respect the requested threshold** without hiding genuinely serious issues
6. **Do a boundary pass** for problems that only show up between slices, such as contract drift, ordering problems, shared config hazards, or rollout mismatches

---

## Phase 6: Deliver the review

1. Output using `/ai-rpi-protocol/templates/code-review-output-template.md`
2. Keep the review actionable: exact location, why it matters, what to do next
3. Include reviewer focus and validation gaps, not just issue text
4. Add trackable action items when the review is large enough to benefit
5. Offer persistence only when it helps handoff or follow-up work
6. If the review session also produced fixes or changed files in the workspace, suggest adding and committing those changes with a very concise one-line commit message
7. End with the review gate

---

## Phase 7: Follow-up fixes

If the user wants fixes:
1. implement the agreed fixes
2. re-run the cheap certainty checks
3. re-review changed areas in fresh context
4. capture repeatable lessons in `/ai-rpi-protocol_project-info/user-preferences.md` only when they are truly durable

---

## Where this skill adds the most value

- merge-facing review
- AI-generated changes that need a real second pass
- cross-file features or refactors where one-pass review will miss things
- high-risk surfaces such as auth, migrations, external integrations, and governed data paths

Practical rule:
- once the change is too broad for one careful pass, partition it

---

## Guardrails

- **Fresh context over self-approval** — avoid reviewing your own implementation in the same reasoning stream
- **Evidence over vibes** — every meaningful finding needs concrete anchors
- **Stop when signal drops** — don't keep widening into low-value nitpicks
- **Checks still matter** — if a proposed fix breaks the project checks, do not bless it
- **Use project context deliberately** — apply relevant preferences, standards, memory, and constraints
- **No ceremonial approval** — the point is to improve judgment, not to generate review-shaped text
