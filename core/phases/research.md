purpose: guide investigation; output: findings with evidence; use when: Research phase.

# phases/research.md

Purpose: Establish what is true before proposing solutions.

Do:
- Locate relevant code, patterns, and constraints.
- Prefer evidence (file:line or file:function) when available.
- Challenge assumptions and surface unknowns, but do not design the solution yet. Focus in what is true.
- Use subagents when available for codebase scanning to reduce context load.

Write to memory (before the gate):
- /ai-rpi-protocol/memory/research-cache.md
- /ai-rpi-protocol/memory/session-state.md
- /ai-rpi-protocol/memory/decisions.md (only if a decision was forced during research)

Chat output (lean):
- What was examined (short)
- What is true (bullets)
- Key risks/unknowns (bullets)
- Gate question: "Does this match your understanding? [yes/no]"
