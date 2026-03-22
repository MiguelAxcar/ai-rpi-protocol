purpose: execute bounded approved work safely and incrementally; output: changes aligned to plan and repo patterns; use when: implementation is approved and needed.

# Skill: implement-change

Use this skill to carry out approved work with minimal drift.

Focus:
- bounded execution
- minimal diffs
- alignment with existing patterns
- continuous checks while moving

Use when:
- the task needs actual code or config changes
- planning or task framing is already sufficient

Do not use when:
- research or planning still has blocking gaps
- the request should stop before execution

Typical outputs:
- changed files
- validation notes
- blockers or deviations if they appear

## Agent leverage (trigger-based)

Pre-implementation:
- `/ai-rpi-protocol/agents/codebase-mapper.md` when blast radius or file boundaries are still unclear
- `/ai-rpi-protocol/agents/standards-discovery.md` when project conventions are unclear in the target area

During implementation:
- `/ai-rpi-protocol/agents/debugger.md` when failure cause is not settled
- `/ai-rpi-protocol/agents/challenger.md` when the implementation drifts from plan or becomes over-complex

Post-implementation validation lenses:
- `/ai-rpi-protocol/agents/code-reviewer.md` for correctness and maintainability on non-trivial changes
- `/ai-rpi-protocol/agents/code-review/security-reviewer.md` when trust boundaries or sensitive data are involved
- `/ai-rpi-protocol/agents/performance-reviewer.md` when hot paths/scale risk are plausible
- `/ai-rpi-protocol/agents/packaging-reviewer.md` when a reviewer-focused handoff is needed

Suggested invocation shape:
```text
Task: Implement approved change with minimal drift.
Target: [files/modules]
Plan anchor: [approved plan summary]
Return: Changed files, deviations, validation evidence, and residual risks.
```
