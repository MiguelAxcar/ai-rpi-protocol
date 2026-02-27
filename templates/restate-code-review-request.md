purpose: restate code review request; output: scoped review spec; use when: user asks to review, audit, or examine code.

# Restate Code Review Request

**When to use:** User asks to review, check, audit, or examine code for quality, patterns, security, or performance. Use BEFORE Phase R on non-trivial reviews.

## Format

**Request:** [One sentence describing what the user wants reviewed]

**Target:** [File(s), module(s), or PR being reviewed]

**Review focus:**
- [Focus area 1 — e.g., security, patterns, performance, general quality]
- [Focus area 2]

**Out of scope:**
- [What NOT to review — e.g., test files, generated code, unrelated modules]

**Severity threshold:** [Flag everything / significant issues only / critical only]

**Expected outcome:**
- [e.g., list of issues with fix suggestions]
- [e.g., review only, no fixes needed]

**Questions:**
1. [Question about scope/focus preferences]
(...)

**Next:** I'll read the code, surface issues with evidence, then advise on each with options and trade-offs. When project-info exists, I'll apply `custom-instructions.md` so the review aligns with your stated preferences.

Does this match what you want? [yes/no/adjustments]
