purpose: define subagent invocation; output: when and how to call subagents proportionally; use when: a specialist delegated worker may add leverage.

# Subagent system

Some IDEs and AI tools support subagents — specialist delegated workers that run in a separate context and return results. This file describes when and how to use them within AI-RPI.

## What subagents are

Subagents are specialist delegated workers with fresh context.

Core distinction:
- **Skills** are reusable workflows
- **Subagents** are specialist workers

Subagents help keep the main conversation focused while adding perspective, isolation, specialization, or parallelism.

Not all IDEs support subagents. If the current environment doesn't, do the research directly — the workflow is the same, just without the delegation.

## Why subagents matter

Every file read and every search in the main agent competes for attention with protocol rules, conversation history, and decision context. Subagents keep the main context window cleaner by moving focused work into a fresh context and returning structured results.

For complex problems, use subagents when they add real leverage. One focused task per subagent produces better results than one agent juggling many concerns. Think of subagents as a way to scale work without polluting context.

Subagents exist for fresh perspective, not ceremony.

## Core subagent set

AI-RPI keeps a small, specialized core set.

| Subagent | File | Focus |
|----------|------|-------|
| `codebase-mapper` | `/ai-rpi-protocol/agents/codebase-mapper.md` | relevant modules, patterns, and impact surfaces |
| `challenger` | `/ai-rpi-protocol/agents/challenger.md` | assumptions, trade-offs, drift, and false certainty |
| `architecture-reviewer` | `/ai-rpi-protocol/agents/code-review/architecture-reviewer.md` | boundaries, interfaces, and architectural fit |
| `code-reviewer` | `/ai-rpi-protocol/agents/code-reviewer.md` | correctness, maintainability, clarity, and reviewer readiness |
| `debugger` | `/ai-rpi-protocol/agents/debugger.md` | likely root causes and failure paths |
| `performance-reviewer` | `/ai-rpi-protocol/agents/performance-reviewer.md` | hot paths, efficiency, and scale implications |
| `security-reviewer` | `/ai-rpi-protocol/agents/code-review/security-reviewer.md` | trust boundaries, auth, permissions, and misuse |
| `documentation-researcher` | `/ai-rpi-protocol/agents/documentation-researcher.md` | current external docs and references |
| `packaging-reviewer` | `/ai-rpi-protocol/agents/packaging-reviewer.md` | reviewability and handoff quality |

## Extended specialist set

These are narrower specialists that add signal for specific contexts:

| Subagent | File | Focus |
|----------|------|-------|
| `web-researcher` | `/ai-rpi-protocol/agents/web-researcher.md` | web documentation, advisories, and recency-sensitive external facts |
| `standards-discovery` | `/ai-rpi-protocol/agents/standards-discovery.md` | discover local conventions and inferred standards before review/implementation |
| `conventions-reviewer` | `/ai-rpi-protocol/agents/code-review/conventions-reviewer.md` | convention drift against discovered standards |
| `patterns-reviewer` | `/ai-rpi-protocol/agents/code-review/patterns-reviewer.md` | naming/style/pattern consistency |
| `test-quality-reviewer` | `/ai-rpi-protocol/agents/code-review/test-quality-reviewer.md` | test validity and false-confidence detection |
| `documentation-reviewer` | `/ai-rpi-protocol/agents/code-review/documentation-reviewer.md` | docs-code sync and documentation risk |

Use these when their perspective materially changes the decision quality.

## Selection rules

Use a subagent when it clearly adds one of these:
- fresh perspective
- context isolation
- specialist knowledge
- parallel leverage

Avoid a subagent when:
- the next step is still local and clear
- the worker would duplicate the main thread without adding signal
- the task is so small that delegation is slower than just doing the work

## How to invoke

1. Determine the exact question or job to delegate.
2. Pick the smallest useful subagent.
3. Pass only the minimum context needed.
4. Define the expected output shape.
5. Use the result immediately.

If the IDE doesn't support subagents, follow the same workflow directly.

## Good delegation

Good delegation sounds like this:
- "Map the relevant modules for token refresh and identify the likely blast radius."
- "Challenge this plan for hidden migration risk and unnecessary complexity."
- "Review this change for architecture drift and long-term maintenance cost."

Bad delegation sounds like this:
- "Look around and tell me what you think."
- "Do the whole task."
- "Review everything."

## Mode and depth behavior

Mode and Depth influence whether delegation is likely to help, but they do not force it.

Guideline:
- Minimal: stay main-thread first; use one subagent only if it clearly prevents rework
- Balanced: one focused subagent is common when research, challenge, or review would otherwise sprawl
- Full: multiple specialists are acceptable when risk, uncertainty, or reviewer needs justify them

Keep the main agent responsible for synthesis and user-facing output.

## Challenger as a first-class differentiator

The challenger is a generalist counterweight, not a narrow phase specialist.

Use the challenger to:
- pressure weak assumptions
- expose hidden trade-offs
- reduce overconfidence
- prevent unnecessary complexity

The challenger should improve judgment, not create friction for its own sake.

## Rules

- only invoke when the delegation justifies itself
- prefer one sharply scoped subagent over many vague ones
- use results immediately
- keep delegation prompts specific and outcome-oriented
- subagent findings should include evidence and references when possible

## Adding new subagents

1. Create file in `/ai-rpi-protocol/agents/[name].md`
2. Keep it broad and durable; do not create a narrow worker for every tiny pattern
3. Structure: purpose, when to invoke, return format
4. Add to this guide and to `file-index.md`
