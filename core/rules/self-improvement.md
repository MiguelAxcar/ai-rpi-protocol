purpose: learn from mistakes across sessions; output: lessons written to memory; use when: user corrects the AI or points out a mistake.

# Self-improvement loop

The protocol tracks what happened (metrics-log) but that alone does not prevent repeating mistakes. This rule closes the loop: when the user corrects you, capture the lesson so it can inform future sessions.

## Trigger

This rule fires when any of these happen:
- The user says you are wrong
- The user asks you to redo something
- The user points out a mistake, misunderstanding, or missed requirement
- The user adjusts your output in a way that reveals a pattern you should have caught

## Action

Append to `/ai-rpi-protocol/memory/lessons.md`:

```
### [Date] — [Short description of mistake]

**What happened:** [What you did wrong — one sentence]
**Root cause:** [Why it happened — wrong assumption, skipped step, misread code, pattern not recognized]
**Prevention:** [Rule for yourself to prevent this in the future]
```

Keep entries short and specific. A prevention rule like "be more careful" is useless. A prevention rule like "when modifying auth middleware, always check if rate limiting is attached" is useful.

## Session start

If `lessons.md` exists and has entries:
- Scan it at session start (or when loading memory for a resuming session)
- If any lessons are relevant to the current task type, keep them in mind
- You do not need to mention lessons to the user unless one directly prevents a mistake you were about to make

## Rules

- **Silent operation.** Do not announce "I'm writing a lesson." Just write it. The user should not be interrupted by the learning process.
- **No blocking.** If you cannot write to the file, continue normally. Lessons are valuable but never blocking.
- **Specificity over volume.** One specific lesson beats five vague ones. If a correction does not reveal a repeatable pattern, skip it.
- **Lessons are additive.** Never delete or overwrite previous lessons. Append only.
- **Periodic review.** If lessons.md grows beyond ~20 entries, consolidate: merge similar lessons, remove ones that are now obvious, and keep the file lean.
