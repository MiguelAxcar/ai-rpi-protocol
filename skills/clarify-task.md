purpose: sharpen vague asks, constraints, and success criteria; output: scoped task framing; use when: the request is ambiguous, underspecified, or drifting.

# Skill: clarify-task

Use this skill to sharpen what the work actually is before wider research or execution.

Focus:
- identify missing constraints
- align on success criteria
- reduce ambiguity and drift
- expose blocking unknowns early

Use when:
- the ask is vague
- multiple interpretations are plausible
- the task is likely to drift without sharper framing

Do not use when:
- the task is already crisp and mechanical
- clarification would add noise instead of safety

Typical outputs:
- restated task
- constraints list
- success criteria
- open questions only when truly needed

## Agent leverage (use when helpful)

Primary subagent:
- `/ai-rpi-protocol/agents/challenger.md` when assumptions conflict or the ask sounds overconfident

Conditional subagents:
- `/ai-rpi-protocol/agents/codebase-mapper.md` when ambiguity depends on how the repo actually behaves
- `/ai-rpi-protocol/agents/standards-discovery.md` when conventions are unclear and they affect interpretation
- `/ai-rpi-protocol/agents/documentation-researcher.md` when clarification depends on external specs/docs

Suggested invocation shape:
```text
Task: Clarify this request into an implementation-safe scope.
Target: [user request]
Focus: [ambiguities, constraints, success criteria]
Return: Restated scope, blocking unknowns, and recommended assumptions.
```
