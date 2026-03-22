purpose: produce technical validation evidence against intent and behavior; output: validation findings, confidence, and gaps; use when: code changed or a review needs technical confirmation.

# Skill: verify-change

Use this skill to confirm that the result matches the intent, not just that it compiles or looks plausible.

Focus:
- behavior against upstream intent
- tests, builds, and other checks
- acceptance mapping against the request or plan
- confidence and gaps between expected and actual results

Use when:
- code or config changed
- a review needs validation evidence

Do not use when:
- nothing material changed
- verification would duplicate already sufficient evidence

Typical outputs:
- validation results
- confidence level
- remaining gaps
- reviewer focus for risky areas

## Validation layers

1. Deterministic checks:
- build/typecheck/lint/tests/security scans as applicable

2. Behavior checks:
- acceptance mapping against request/plan
- edge/error path validation where risk is non-trivial

3. Specialist checks (when warranted):
- targeted agent passes to increase signal before final claim

## Agent leverage (trigger-based)

Baseline for non-trivial changes:
- `/ai-rpi-protocol/agents/code-reviewer.md`

Risk-specific lenses:
- `/ai-rpi-protocol/agents/code-review/security-reviewer.md` for auth/permissions/secrets/governed data
- `/ai-rpi-protocol/agents/performance-reviewer.md` for hot paths, throughput, or latency risk
- `/ai-rpi-protocol/agents/debugger.md` when failing behavior is still unclear

Review-depth lenses:
- `/ai-rpi-protocol/agents/code-review/test-quality-reviewer.md` when confidence depends heavily on tests
- `/ai-rpi-protocol/agents/code-review/conventions-reviewer.md` or `/ai-rpi-protocol/agents/code-review/patterns-reviewer.md` when convention drift is plausible
- `/ai-rpi-protocol/agents/code-review/documentation-reviewer.md` when behavior/interface changes may desync docs
- `/ai-rpi-protocol/agents/challenger.md` when confidence appears higher than evidence quality

Packaging support:
- `/ai-rpi-protocol/agents/packaging-reviewer.md` for reviewer-ready validation summaries
