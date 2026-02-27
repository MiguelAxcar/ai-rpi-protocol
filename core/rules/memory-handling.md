purpose: memory workflow; output: what to write and when; use when: phase transitions or decision points.

# Memory handling

Memory is file-based state that helps maintain context across phases and sessions. It is not automatic — the AI writes to files, and those files must be explicitly read to be useful later.

## When memory is required

Memory writes are required in **Thoughtful** and **Comprehensive** modes. In **Quick** and **Streamlined** modes, memory is optional — use it when the task is complex enough that losing context would cause rework.

## How it actually works

Memory is markdown files written to disk. They persist between sessions only if:
1. The AI writes them during the current session
2. The AI (or user) reads them at the start of the next session

This is not automatic recall. It is structured note-taking. Its value is proportional to how well the notes are written and how consistently they are read back.

## Rules

1. **Read memory at session start** if the user says "resume" or "load state", or if memory files exist and the task seems related.

2. **Write to memory before phase transitions** in modes that require it. Keep writes lean — store enough to reconstruct context, not a transcript.

3. **Don't block the user for memory operations.** If memory writes were missed, silently write them before the next gate. If reconstruction is impossible, note the gap and continue.

## Memory files

| File | Purpose | Write when |
|------|---------|------------|
| `/ai-rpi-protocol/memory/session-state.md` | Current task and phase status | Phase transitions, session end |
| `/ai-rpi-protocol/memory/research-cache.md` | Research findings with evidence | Research completed |
| `/ai-rpi-protocol/memory/plans/{task}-plan.md` | Approved plan | Planning approved |
| `/ai-rpi-protocol/memory/decisions.md` | Decisions and rationale | Any meaningful decision |
| `/ai-rpi-protocol/memory/metrics-log.md` | Task metrics (tokens, catches, rework) | Implementation completed |
| `/ai-rpi-protocol/memory/lessons.md` | Mistake patterns and prevention rules | After user corrections |

## RPI Phase exit checklist

Research exit:
* Update `research-cache.md` and `session-state.md`

Planning exit:
* Write approved plan to `plans/{task}-plan.md`
* Append key decisions to `decisions.md`
* Update `session-state.md`

Implementation exit:
* Mark completion in `session-state.md`
* Append any new decisions to `decisions.md`
* Append metrics row to `metrics-log.md` (tokens used, tokens saved estimate, catches, rework)

## User commands

* "save state" or "checkpoint": write `session-state.md` and any pending artifacts
* "load state" or "resume": read `session-state.md` and continue from there
* "show decisions": summarize from `decisions.md`
* "clear memory": archive current files and start fresh (don't delete without asking)
* "show metrics": read `metrics-log.md` and summarize patterns — total tasks, rework rate, tokens saved, most common catches, adjustment recommendations

## Recovery

If memory was not written when it should have been:
1. Reconstruct from conversation context if possible
2. Write the missing files
3. Continue without interrupting the user

If reconstruction is impossible, note the gap in `session-state.md` and move on. Memory is important but never blocking.

## Repo policy

Memory can be personal (gitignored) or shared (committed). Follow the repo policy. If the repo has no policy, ask once and follow that decision.

## Context refresh handoff

When context gets long or drifty:

1. Stop generating new output
2. Persist current state to memory files
3. Produce a lean handoff summary (5-9 bullets max): task goal, current phase, confirmed facts, constraints, chosen direction, next steps
4. Continue from the summary + memory files only
5. If the user wants a completely new topic, offer a clean handoff prompt for a new chat
