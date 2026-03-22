purpose: stress-test a direction before or during planning; output: trade-offs, risks, drift warnings, and better alternatives; use when: the plan needs deliberate challenge.

# Skill: challenge-plan

Use this skill to challenge assumptions, expose trade-offs, and surface hidden complexity before execution hardens.

Focus:
- weak specs
- unjustified assumptions
- overengineering and under-scoping
- hidden costs, side-effects, and drift

Use when:
- the task has real design or delivery choices
- confidence looks higher than the evidence justifies

Do not use when:
- there is no real plan or trade-off to challenge yet
- the task is purely mechanical and reversible

Typical outputs:
- alternatives
- risks and hidden costs
- recommended simplifications or corrections

## Agent leverage (use when helpful)

Primary subagent:
- `/ai-rpi-protocol/agents/challenger.md` for an independent pressure test

Conditional subagents:
- `/ai-rpi-protocol/agents/code-review/architecture-reviewer.md` when boundaries/interfaces are part of the decision
- `/ai-rpi-protocol/agents/codebase-mapper.md` when options rely on uncertain repo behavior
- `/ai-rpi-protocol/agents/standards-discovery.md` when plan quality depends on local conventions
- `/ai-rpi-protocol/agents/documentation-researcher.md` when external behavior/standards shape trade-offs

Suggested invocation shape:
```text
Task: Stress-test this plan and surface better alternatives.
Target: [plan/options]
Focus: [risk, complexity, architecture fit, rollout]
Return: Ranked risks, weak assumptions, and concrete option adjustments.
```
