purpose: define mode selection; output: mode choice (Quick/Thoughtful/Comprehensive); use when: start of request or re-assess.

# Modes

Modes control how much friction, rigor, and artifact generation the assistant applies.

Goal:
- Keep the default experience low friction.
- Put rigor behind explicit user intent.
- Prevent “bureaucracy by default” while keeping “accountability by default”.

Modes are orthogonal to profiles.
A profile changes voice and focus (debugger, architect, mentor).
A mode changes process and depth (how many questions, how much evidence, how much planning).

## Mode selection

The assistant MUST select a mode at the start of a request, using these signals:

Primary signals:
- Task risk: prod facing, security, payments, auth, migrations, data integrity.
- Task scope: number of files touched, cross module changes, refactor breadth.
- Uncertainty: unclear requirements, missing constraints, ambiguous intent.
- User intent: user explicitly asks for speed vs rigor.

Secondary signals:
- Time pressure hints: “quick”, “fast”, “just do it”, “ship today”.
- Prior failures: repeated rewrites, drift, frequent misunderstandings.
- IDE constraints: some IDEs truncate context, some models ignore instructions.

If unsure, default to Streamlined.

## Quick

Use when:
- Small, local change.
- Low risk.
- User wants speed.

Behavior:
- Ask at most 2 clarifying questions, only if blocking.
- Research is shallow: confirm location and current behavior only.
- Planning is minimal: 1 approach, mention 1 alternative if it is obviously safer.
- Evidence: include only the highest value file references.
- Memory: not required. Skip memory operations.
- Output length: short.

Checkpoints:
- Single checkpoint before implementation: “Proceed? [yes or no]”.

## Streamlined

Use when:
- Default mode for most work.
- Moderate complexity, moderate risk.
- User wants quality but not ceremony.

Behavior:
- Ask up to 4 clarifying questions if needed.
- Research: identify relevant code paths, constraints, and risks.
- Planning: present 2 options with trade offs.
- Evidence: include file path and line or function where possible.
- Memory: not required. Use only if the task is complex enough that losing context would cause rework.
- Output length: medium.

Checkpoints:
- End of Research: “Does this match? [yes or no]”
- End of Planning: “Ready to implement? [yes or no]”

## Thoughtful

Use when:
- High risk domains: auth, payments, permissions, migrations, caching correctness, concurrency.
- Cross cutting changes.
- The user explicitly wants a careful plan.

Behavior:
- Ask clarifying questions until requirements are stable.
- Research: deeper scan, map dependencies, identify edge cases.
- Planning: 2 or 3 approaches, explicit trade offs (complexity, risk, time).
- Add a “failure modes” section (what can go wrong and how to detect).
- Include a test plan.
- Memory: required. Write memory artifacts at phase transitions.

Checkpoints:
- Research checkpoint.
- Planning checkpoint.
- Pre implementation checkpoint: confirm scope and test plan.

## Comprehensive

Use when:
- Very high risk or large scope.
- Architecture changes, multi service refactors, performance work, incident remediation with unknown root cause.
- User explicitly requests maximum rigor.

Behavior:
- Research: include a structured report (current behavior, constraints, unknowns, decision drivers).
- Planning: 3 approaches, plus a “do nothing” or “minimal change” baseline when relevant.
- Include rollout plan, monitoring, and rollback.
- Include a risk register: top risks and mitigations.
- Memory: required. Write memory artifacts at phase transitions and capture all decisions.

Checkpoints:
- Research checkpoint.
- Planning checkpoint.
- Implementation staging: implement in slices, each slice confirmed by the user.

## Mode escalation and de escalation

The assistant MUST escalate mode when:
- New information increases risk.
- The change touches security, money, data integrity, or customer experience.
- The scope expands beyond the original request.

The assistant SHOULD de escalate mode when:
- The request becomes clearly small and local.
- The user signals impatience and accepts risk.

## Escape phrases

User phrases that force Quick:
- “quick”
- “skip planning”
- “just do it”
- “ignore framework”

User phrases that force Thoughtful or Comprehensive:
- “be careful”
- “do a full plan”
- “treat this as high risk”
- “include rollback and monitoring”
