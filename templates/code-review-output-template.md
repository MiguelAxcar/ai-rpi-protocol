purpose: code review per-issue output template; output: structured advice per issue; use when: Planning phase of a code review task.

# Code Review Output Template

**Use this template during Planning for code review tasks.** For each issue found in Research, produce one entry. Skip the template for issues the user explicitly deprioritized.

---

# Code Review: [File or Module Name]

**Date:** [Date]
**Issues found:** [N]

---

## Issue [N]: [Short title]

**Location:** `file:line` or `file:function`
**Severity:** Critical / High / Medium / Low

### What's wrong

[1-3 sentences: what the issue is and where it occurs. Cite evidence.]

### Why it matters

[1-3 sentences: why this isn't a good idea, what breaks, degrades, becomes harder to maintain, etc Be specific — not "this is bad practice" but "this causes X when Y happens."]

### Options

**Option 1: [Approach name]**
- How: [What to change]
- Pros: [Benefits]
- Cons: [Drawbacks]
- Effort: Low / Medium / High

**Option 2: [Alternative approach]**
- How: [What to change]
- Pros: [Benefits]
- Cons: [Drawbacks]
- Effort: Low / Medium / High

### Suggested approach

**[Option N]** — [1-2 sentences: why this is the recommended path, considering the project context and trade-offs above.]

---

## Summary

| # | Issue | Severity | Suggested approach | Effort |
|---|-------|----------|--------------------|--------|
| 1 | [title] | [sev] | [approach] | [effort] |
| 2 | [title] | [sev] | [approach] | [effort] |

**Gate:** Which issues do you want to fix? Want to adjust any of the suggested approaches? [approve all / select specific / adjust]
