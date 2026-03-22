purpose: memory workflow; output: what to write and when; use when: phase transitions or decision points.

# Memory handling

Memory is file-based state that helps maintain context across phases and sessions. It is not automatic — the AI writes to files, and those files must be explicitly read to be useful later.

Persistent project context is separate from session memory.

Always treat these project-scoped files as durable context when they exist:
- `/ai-rpi-protocol_project-info/memory.md`
- `/ai-rpi-protocol_project-info/user-preferences.md`

Those files survive sessions and protocol upgrades. The files in `/ai-rpi-protocol/memory/` are session and workflow memory.

If the project-info surface exists but `/ai-rpi-protocol_project-info/memory.md` does not, create it before the next durable memory write instead of repeatedly treating it as absent.

## When memory is required

Memory writes are required at **full** Depth. In **minimal** and **balanced** depth, memory is optional — use it when the task is complex enough that losing context would cause rework.

## How it actually works

Memory is markdown files written to disk. They persist between sessions only if:
1. The AI writes them during the current session
2. The AI (or user) reads them at the start of the next session

This is not automatic recall. It is structured note-taking. Its value is proportional to how well the notes are written and how consistently they are read back.

## Rules

1. **Read memory at session start** if the user says "resume" or "load state", or if memory files exist and the task seems related.

2. **Write to memory before phase transitions** in modes that require it. Keep writes lean — store enough to reconstruct context, not a transcript.

3. **Don't block the user for memory operations.** If memory writes were missed, silently write them before the next gate. If reconstruction is impossible, note the gap and continue.
4. **Use an output-triggered memory check.** Before user-facing output, ask: did this turn reveal a repeatable project-level lesson, durable fact, or stable workflow preference worth keeping? If yes, write it. If `memory.md` is missing, create it first.

## Memory files

| File | Purpose | Write when |
|------|---------|------------|
| `/ai-rpi-protocol/memory/session-state.md` | Current task and phase status | Phase transitions, session end |
| `/ai-rpi-protocol/memory/research-cache.md` | Research findings with evidence | Research completed |
| `{workspace_root}/artifacts/shaping/{date}-{artifact}.md` | Shareable shaping artifact | Planning approved (preferred for reviewable shaping docs) |
| `{workspace_root}/artifacts/delivery/{date}-{artifact}.md` | Shareable delivery artifact | Implementation or review packaging when saved output is useful |
| `/ai-rpi-protocol/memory/plans/{task}-plan.md` | Approved plan (session) | Planning approved (fallback when plans/ not used) |
| `/ai-rpi-protocol/memory/decisions.md` | Decisions and rationale | Any meaningful decision |
| `/ai-rpi-protocol/memory/metrics-log.md` | Lightweight task-quality signals and adjustment hints | Implementation completed when a lean metrics row would be useful |
| `/ai-rpi-protocol_project-info/memory.md` | Durable project memory, including stable lessons worth remembering across sessions | When a repeatable project-level lesson or durable fact should persist |

## RPI Phase exit checklist

Research exit:
* Update `research-cache.md` and `session-state.md`

Planning exit:
* Write the approved planning artifact to `memory/plans/{task}-plan.md` for session persistence, or `{workspace_root}/artifacts/shaping/` for shareable shaping artifacts per planning-prd-techspec-guidance
* Append key decisions to `decisions.md`
* Update `session-state.md`

Implementation exit:
* Mark completion in `session-state.md`
* Append any new decisions to `decisions.md`
* Save any worthwhile delivery artifact to `{workspace_root}/artifacts/delivery/` when it should survive the session
* Append a lean metrics row to `metrics-log.md` when it would help reveal outcome, noise, correction, or rigor patterns

## User commands

* "save state" or "checkpoint": write `session-state.md` and any pending artifacts
* "load state" or "resume": read `session-state.md` and continue from there
* "show decisions": summarize from `decisions.md`
* "clear memory": archive current files and start fresh (don't delete without asking)
* "show metrics": read `metrics-log.md` and summarize patterns — outcome quality, noise, corrections, rigor calibration, and adjustment recommendations

## Recovery

If memory was not written when it should have been:
1. Reconstruct from conversation context if possible
2. Write the missing files
3. Continue without interrupting the user

If reconstruction is impossible, note the gap in `session-state.md` and move on. Memory is important but never blocking.

## Durable memory posture

Durable project memory should be treated as conceptually always available.

Rules:
- keep project memory concise
- use it to improve future behavior, not to store a transcript of mistakes
- prefer representative patterns over noisy accumulation
- store only project-level, reusable memory there
- if a lesson is likely to matter again, save it instead of assuming it will be remembered

## Repo policy

Memory can be personal (gitignored) or shared (committed). Follow the repo policy. If the repo has no policy, ask once and follow that decision.

## Context refresh handoff

When context gets long or drifty:

1. Stop generating new output
2. Persist current state to memory files
3. Produce a lean handoff summary (5-9 bullets max): task goal, current phase, confirmed facts, constraints, chosen direction, next steps
4. Continue from the summary + memory files only
5. If the user wants a completely new topic, offer a clean handoff prompt for a new chat
