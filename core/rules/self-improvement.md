purpose: learn from mistakes across sessions; output: concise lessons written to memory; use when: user corrects the AI or points out a mistake.

# Self-improvement loop

The protocol should improve deliberately from real cases, not only intuition.

Metrics alone do not prevent repeated mistakes. This rule closes the loop: when the user corrects you, capture the lesson so it can inform future sessions.

## Trigger

This rule fires when any of these happen:
- The user says you are wrong
- The user asks you to redo something
- The user points out a mistake, misunderstanding, or missed requirement
- The user adjusts your output in a way that reveals a pattern you should have caught
- The user indicates the protocol was too heavy, too light, too unclear, or badly timed

## Action

Append to `/ai-rpi-protocol_project-info/memory.md` when the lesson is durable and project-scoped:

```
### [Date] — [Short description of mistake]

**What happened:** [What you did wrong — one sentence]
**Root cause:** [Why it happened — wrong assumption, skipped step, misread code, pattern not recognized]
**Prevention:** [Rule for yourself to prevent this in the future]
```

Keep entries short and specific. A prevention rule like "be more careful" is useless. A prevention rule like "when modifying auth middleware, always check if rate limiting is attached" is useful.

If `/ai-rpi-protocol_project-info/memory.md` is missing but the project-info surface exists:
- create it first
- then append the lesson

Lessons should stay useful for future cases:
- capture recurring patterns, not every tiny imperfection
- prefer one strong lesson over many weak ones
- note whether the mistake was about outcome quality, protocol quality, or both

## Session start

If `/ai-rpi-protocol_project-info/memory.md` exists and has relevant entries:
- scan it at session start, or when loading memory for a resuming session
- treat relevant durable memory as conceptually always available guidance
- if any lessons are relevant to the current task type, keep them in mind
- you do not need to mention lessons to the user unless one directly prevents a mistake you were about to make

## Rules

- **Silent operation.** Do not announce "I'm writing a lesson." Just write it. The user should not be interrupted by the learning process.
- **No blocking.** If you cannot write to the file, continue normally. Lessons are valuable but never blocking.
- **Specificity over volume.** One specific lesson beats five vague ones. If a correction does not reveal a repeatable pattern, skip it.
- **Lessons are additive.** Never delete or overwrite previous lessons. Append only.
- **Periodic review.** If project memory grows beyond what stays useful, consolidate: merge similar lessons, remove ones that are now obvious, and keep the file lean.
- **Occasional escalation.** If a correction reveals a meaningful protocol gap or repeated failure mode, it may be worth suggesting a GitHub issue or benchmark case — only when genuinely useful.
- **Bias toward retention when repetition is likely.** If the same mistake, preference, or pitfall is likely to recur, save it rather than hoping it stays in working memory.
