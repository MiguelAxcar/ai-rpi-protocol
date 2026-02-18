purpose: execute approved plan; output: working code + finish discipline; use when: Implement phase.

# phases/implementation.md

Purpose: Execute the approved plan with minimal drift.

Do:
- Implement the approved plan. Do not introduce new scope.
- If a deviation is needed, stop and ask for approval before changing the plan.
- Maintain finish discipline (tests, lint/typecheck where applicable, no surprise churn).

Write to memory (before the final checkpoint):
- /ai-rpi-protocol/memory/session-state.md
- /ai-rpi-protocol/memory/decisions.md (only if new decisions occurred)
- /ai-rpi-protocol/memory/metrics-log.md — append one row with task metrics (see below)

Metrics row (append to metrics-log.md at task completion):
- Date, task name, mode used
- Gate adjustments: how many times user said "no" or asked for changes at a gate
- Escapes: how many times user bypassed the protocol
- Catches: what the protocol caught (wrong assumptions, hallucinations flagged, risks surfaced)
- Tokens used: rough estimate from conversation length (messages × avg response size)
- Tokens saved (est.): estimate based on catches — minor catch ~500-1k, medium ~2-5k, major ~5-15k tokens of rework avoided
- Rework: did anything need to be redone after implementation?
- Notes: one-line summary of what the protocol caught or missed

Chat output (lean):
- What changed (bullets)
- Where (files)
- How verified (tests/lint/commands, if run)
- Final checkpoint: "Complete. Next? [done/review/fix]"
