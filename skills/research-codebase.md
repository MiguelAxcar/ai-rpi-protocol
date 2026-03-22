purpose: inspect relevant repo truth before decisions; output: targeted findings with evidence; use when: the next decision depends on codebase reality.

# Skill: research-codebase

Use this skill to inspect relevant files, patterns, architecture, dependencies, and evidence without widening more than necessary.

Focus:
- target the smallest relevant slice first
- map files, flows, constraints, and impact surfaces
- surface evidence, not guesses

Use when:
- repo truth matters for the next step
- patterns, boundaries, or dependencies are still unclear

Do not use when:
- the answer is already verified locally
- more reading would not change the decision

Typical outputs:
- key files and why they matter
- current behavior and constraints
- risks, assumptions, and escalation triggers

## Execution model

Use the lightest path first:
1. Main-thread local reads for small, clear questions
2. Delegate to `/ai-rpi-protocol/agents/codebase-mapper.md` when mapping or deep investigation would otherwise sprawl
3. Add `/ai-rpi-protocol/agents/debugger.md` when diagnosis, not mapping, is the primary research job
4. Add `/ai-rpi-protocol/agents/standards-discovery.md` when conventions materially affect the decision
5. Add `/ai-rpi-protocol/agents/documentation-researcher.md` only when repo evidence is insufficient
6. Add `/ai-rpi-protocol/agents/web-researcher.md` only for external/current information not available in repo docs

## Delegation triggers for Codebase Mapper

Delegate when any of these is true:
- research likely spans many files or modules
- boundaries and blast radius are unclear
- diagnosis needs a fresh, isolated pass
- you need explicit pattern matching against adjacent implementations

Suggested delegation shape:
```
Task: Map or deeply investigate the codebase for [objective].
Target: [feature/module/flow]
Depth: quick | deep
Return: Structured findings with file:line evidence and likely impact surface.
```
