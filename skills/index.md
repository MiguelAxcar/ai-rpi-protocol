purpose: skills registry and operating model; output: core skill set, selection rules, and specialized examples; use when: every conversation, loaded from AGENTS.md.

# Skills

Skills are reusable procedural know-how. A skill is **how to do a kind of work**.

Skills are workflows, not workers. They can run in the main thread or use a subagent when fresh context or specialist perspective would help.

---

## Core distinction

- **Skills** = reusable workflows
- **Subagents** = specialist delegated workers with fresh context

Do not blur these concepts.

## How skills work

1. **Detection** — the main agent checks whether a reusable workflow would materially improve the task.
2. **Selection** — the main agent chooses the smallest useful skill set for the current Mode, Depth, and phase.
3. **Execution** — the skill can run in the main thread or use a subagent if fresh perspective, isolation, or specialization helps. Exception: code review requests route to the dedicated multi-agent Code Review workflow.
4. **Presentation** — the main agent returns the useful result, not the full workflow internals.

Rule:
- skills sharpen how work is done
- skills do not automatically force delegation
- skills should stay small in number and broad in meaning
- when a request clearly matches a skill, load that skill file before producing substantive output for that task
- do not produce skill-shaped output without having loaded and followed the matching skill file
- prior familiarity with the codebase is not a valid reason to skip a matched skill
- for code review in particular, prior familiarity is a reason to respect the fresh-context review workflow, not bypass it

---

## Core skill set

| Skill | Purpose | File |
|-------|---------|------|
| `clarify-task` | sharpen vague asks, constraints, and success criteria | `/ai-rpi-protocol/skills/clarify-task.md` |
| `research-codebase` | inspect relevant repo truth before decisions | `/ai-rpi-protocol/skills/research-codebase.md` |
| `challenge-plan` | stress-test a direction before or during planning | `/ai-rpi-protocol/skills/challenge-plan.md` |
| `implement-change` | execute bounded approved work safely and incrementally | `/ai-rpi-protocol/skills/implement-change.md` |
| `verify-change` | produce validation evidence against intent and behavior | `/ai-rpi-protocol/skills/verify-change.md` |
| `package-reviewable-work` | produce reviewer-ready packaging and handoff outputs | `/ai-rpi-protocol/skills/package-reviewable-work.md` |
| `review-code` | compatibility bridge that routes to `code-review` | `/ai-rpi-protocol/skills/review-code.md` |
| `write-tech-spec` | create proportional technical design artifacts | `/ai-rpi-protocol/skills/write-tech-spec.md` |
| `write-prd` | create proportional product requirement artifacts | `/ai-rpi-protocol/skills/write-prd.md` |

## Specialized workflow examples

These deeper examples exist because they add real leverage, not because AI-RPI wants dozens of narrow skills:

| Workflow | Purpose | File |
|----------|---------|------|
| `automated-tests` | deeper test-writing workflow | `/ai-rpi-protocol/skills/automated-tests.md` |
| `code-review` | default multi-agent code review workflow | `/ai-rpi-protocol/skills/code-review.md` |

## Agent leverage map

Use this as a practical routing index so every agent has a clear value path.

| Subagent | Typical entry skills |
|----------|----------------------|
| `codebase-mapper` | `research-codebase`, `write-tech-spec`, `write-prd`, `implement-change`, `code-review` |
| `challenger` | `clarify-task`, `challenge-plan`, `write-tech-spec`, `write-prd`, `verify-change`, `code-review` |
| `debugger` | `research-codebase`, `implement-change`, `verify-change` |
| `documentation-researcher` | `research-codebase`, `write-tech-spec`, `write-prd`, `code-review` |
| `web-researcher` | `research-codebase`, `code-review` (dependency/advisory recency checks) |
| `standards-discovery` | `research-codebase`, `automated-tests`, `write-tech-spec`, `code-review` |
| `code-reviewer` | `verify-change`, `implement-change`, `code-review` |
| `architecture-reviewer` | `challenge-plan`, `write-tech-spec`, `write-prd`, `code-review` |
| `security-reviewer` | `implement-change`, `verify-change`, `code-review` |
| `performance-reviewer` | `implement-change`, `verify-change`, `code-review` |
| `packaging-reviewer` | `package-reviewable-work`, `implement-change`, `verify-change`, `code-review` |
| `conventions-reviewer` | `verify-change`, `code-review` |
| `patterns-reviewer` | `automated-tests`, `verify-change`, `code-review` |
| `test-quality-reviewer` | `automated-tests`, `verify-change`, `code-review` |
| `documentation-reviewer` | `package-reviewable-work`, `verify-change`, `code-review` |

---

## Matching rules

- If the task clearly benefits from a core skill, use it.
- If the user asks to review, audit, or examine code, route to `/ai-rpi-protocol/skills/code-review.md`.
- Skill match is a hard gate, not a stylistic hint. Once the match is clear, load the skill file before producing substantive task output.
- Do not satisfy a matched skill request with ad-hoc inline output that merely resembles the skill's result.
- If the match is ambiguous, ask only when the answer would change the workflow.
- Skills do not replace RPI. They operationalize parts of the loop proportionally.
- Skills apply at all protocol levels, but Depth controls how much of the workflow is actually used.
- Prefer the fewest useful skills. AI-RPI deliberately prefers a small, strong skill set over an explosion of micro-skills.
