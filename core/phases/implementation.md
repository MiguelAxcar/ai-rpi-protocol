purpose: execute approved plan; output: working code + finish discipline; use when: Implement phase.

# phases/implementation.md

Purpose: Execute the approved plan with minimal drift.

Do:
- Implement the approved plan. Do not introduce new scope.
- **Follow project custom instructions:** When `/ai-rpi-protocol_project-info/custom-instructions.md` exists, load it and apply it to every change. Code produced in Implementation must honor those instructions.
- If a deviation is needed, stop and ask for approval before changing the plan.
- If the plan has checkable steps, mark each step complete as you go. Update the plan artifact in memory so progress survives context refreshes.
- Maintain finish discipline (tests, lint/typecheck where applicable, no surprise churn).
- Before presenting implementation results: verify that behavior changed as intended, not just that code compiles. Diff before/after when relevant.
- **Whenever files get changed:** Load and apply `/ai-rpi-protocol/core/rules/on-files-changed.md` — run lint (and typecheck/tests if applicable), check if project-info needs updating, and run the code-generation-rules checklist.

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
- **When the task was code review fixes:** For each fix that reflects a repeatable pattern or preference, suggest one abstract rule the user can add to `custom-instructions.md` (e.g. "Don't use useEffect when [X]; prefer [Y].") and ask: "Want to add any of these to custom-instructions so future code follows them?"
- Final checkpoint: "Complete. Next? [done/review/fix]"
