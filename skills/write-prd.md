purpose: create proportional product requirement artifacts; output: user story, PRD, or related product framing artifact; use when: product intent needs durable clarification.

# Skill: write-prd

Use this skill to capture product intent and success criteria in a durable, reviewable form.

Focus:
- user outcomes
- scope and success criteria
- product trade-offs that shape implementation

Use when:
- feature framing needs a durable artifact
- multiple stakeholders need clearer intent

Before generating a PRD, explain why it is worth the extra weight unless the user already asked for one.

Do not use when:
- the work is purely technical or already well-scoped

Typical outputs:
- user story
- micro PRD
- condensed or full PRD when justified
- PRD paired with a tech spec when product and technical ambiguity both need reviewable artifacts

## Agent leverage (recommended)

Framing and feasibility:
- `/ai-rpi-protocol/agents/challenger.md` to stress-test scope, outcomes, and hidden trade-offs
- `/ai-rpi-protocol/agents/codebase-mapper.md` when feasibility depends on current architecture reality

Cross-functional grounding:
- `/ai-rpi-protocol/agents/documentation-researcher.md` when external behavior/standards influence product constraints
- `/ai-rpi-protocol/agents/code-review/architecture-reviewer.md` when product scope materially affects interfaces and boundaries

Suggested invocation shape:
```text
Task: Produce proportional PRD.
Target: [feature/problem]
Scope: [user story | micro | condensed | full]
Return: user outcomes, constraints, options, acceptance, and rollout risks.
```
