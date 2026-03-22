purpose: create proportional technical design artifacts; output: brief plan, tech spec, or related technical artifact; use when: technical shape needs durable documentation.

# Skill: write-tech-spec

Use this skill to create the lightest technical artifact that still makes the solution reviewable.

Focus:
- technical design clarity
- interfaces, migrations, or system behavior
- enough sequence for safe execution

Use when:
- the work has technical complexity that should survive the chat

Before generating a heavier spec, explain why it is worth the extra weight unless the user already asked for one.

Do not use when:
- a brief plan or direct implementation is sufficient

Typical outputs:
- brief technical plan
- condensed tech spec
- full tech spec when risk warrants it
- ADR / decision memo when the main need is durable decision rationale

## Agent leverage (recommended)

Research and grounding:
- `/ai-rpi-protocol/agents/codebase-mapper.md` (use `Depth: deep` when architecture is cross-cutting)
- `/ai-rpi-protocol/agents/standards-discovery.md` when local conventions should shape structure decisions
- `/ai-rpi-protocol/agents/documentation-researcher.md` when external APIs/libraries materially affect design

Design pressure and challenge:
- `/ai-rpi-protocol/agents/code-review/architecture-reviewer.md` for boundary/interface validation
- `/ai-rpi-protocol/agents/challenger.md` for complexity and rollout-risk pressure testing

Suggested invocation shape:
```text
Task: Produce proportional technical spec.
Target: [feature/system area]
Scope: [brief | condensed | full]
Return: options, trade-offs, recommended shape, sequence, and validation anchors.
```
