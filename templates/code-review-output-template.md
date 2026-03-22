purpose: code review per-issue output template; output: structured advice per issue; use when: Planning phase or Code Review skill multi-agent aggregation.

# Code Review Output Template

**Use this template during Planning for code review tasks, and when aggregating specialist agent findings in the Code Review skill.** For each issue, produce one entry. Skip for issues the user explicitly deprioritized. When multiple agents run, include `**Source:**` (which specialist found it).

Ordering rule:
- Sort issues by severity in the final output summary and action list: Critical, High, Medium, Low

---

# Code Review: [File or Module Name]

**Date:** [Date]
**Issues found:** [N]
**Agents run:** [Security, Conventions, Architecture, Test Quality, Patterns, Documentation — or subset]

---

## Issue [N]: [Short title]

**Location:** `file:line` or `file:function`
**Severity:** Critical / High / Medium / Low
**Source:** [Security | Conventions | Architecture | Test Quality | Patterns | Documentation] — omit if single-agent review
**Confidence:** Low / Medium / High — [why]

### What's wrong

[1-3 sentences: what the issue is and where it occurs. Cite evidence.]

### Why it matters

[1-3 sentences: why this isn't a good idea, what breaks, degrades, becomes harder to maintain, etc Be specific — not "this is bad practice" but "this causes X when Y happens."]

### Validation gap

[What validation evidence is missing, weak, or contradicted? Note acceptance mismatches when relevant.]

### Compliance impact (optional)

[Only include when the issue affects documented regulatory, privacy, residency, audit, contractual, or other compliance constraints. State what boundary, policy, or governed data path is affected.]

### Options

**Option 1: [Approach name]**
- How: [What to change]
- Trade-offs: [What gets better, what gets worse, what complexity or risk shifts]
- Effort: Low / Medium / High

**Option 2: [Alternative approach]**
- How: [What to change]
- Trade-offs: [What gets better, what gets worse, what complexity or risk shifts]
- Effort: Low / Medium / High

### Suggested approach

**[Option N]** — [1-2 sentences: why this is the recommended path in this codebase, considering the trade-offs above.]

### Suggested rule for user-preferences (optional)

If this issue reflects a repeatable pattern or preference (e.g. "don't use X here, use Y"), suggest one abstract rule the user can add to `/ai-rpi-protocol_project-info/user-preferences.md` so future code avoids the same finding. Example: *"Don't use useEffect when [situation X]; prefer [Y]."* Skip if the issue is one-off or not generalizable.

---

## Summary

Sort this table by severity first: Critical, High, Medium, Low.

| # | Issue | Severity | Compliance | Suggested approach | Effort |
|---|-------|----------|------------|--------------------|--------|
| 1 | [title] | [sev] | [optional: GDPR / residency / internal policy / none] | [approach] | [effort] |
| 2 | [title] | [sev] | [optional: PCI-DSS / audit / contract / none] | [approach] | [effort] |

**Suggested additions to user-preferences (optional):** [List any abstract rules suggested per issue that the user may add to `/ai-rpi-protocol_project-info/user-preferences.md` to avoid the same findings in future code.]
**Reviewer focus:** [Where the reviewer should spend attention first and why.]
**Validation gaps:** [What is still thin, inferred, or unverified across the review.]

---

## Action items

Sort action items by severity first, matching the summary.

[ ] Issue 1: [Short title] — [file:line]
[ ] Issue 2: [Short title] — [file:line]
...

---

**Gate:** Which issues do you want to fix? Want to adjust any suggested approaches? [approve all / select specific / adjust]

**Commit suggestion (only when this review session also changed files):** Commit finished - Would you like to add and commit these [N] files?
- [file 1]
- [file 2]
- [file 3]
Commit message: "[very concise 1-line message]"

**Persistence:** Want this review saved to `artifacts/delivery/<date>-review-package-<branch>.md`, `docs/<branch>-code-review.md`, or `plans/<branch>-code-review.md`?
