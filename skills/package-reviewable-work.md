purpose: produce reviewer-ready summaries and delivery artifacts; output: reviewable package, PR narrative, handoff note, validation summary, or related delivery artifact; use when: the outcome needs clean review or transfer.

# Skill: package-reviewable-work

Use this skill to make a result easy to review, hand off, or approve.

Focus:
- who the package is for and what decision they need to make
- why it changed
- what was validated
- how the result maps to acceptance
- what remains uncertain
- confidence level when it matters
- what reviewers should inspect
- clear delivery artifact recommendations when useful

Use when:
- the result needs reviewability or handoff support
- the task is large enough that clean packaging saves time

Do not use when:
- the result is tiny and self-evident

Typical outputs:
- review package
- PR summary
- handoff note
- validation summary
- QA checklist

## Agent leverage (use when helpful)

Primary subagent:
- `/ai-rpi-protocol/agents/packaging-reviewer.md` for narrative tightening and reviewer focus

Conditional subagents:
- `/ai-rpi-protocol/agents/challenger.md` when packaging may hide unresolved trade-offs
- `/ai-rpi-protocol/agents/code-review/documentation-reviewer.md` when docs/readme/api notes may need alignment

Suggested invocation shape:
```text
Task: Prepare reviewer-ready package.
Target: [change summary + validation evidence]
Audience: [reviewer/approver/operator]
Return: concise narrative, focus areas, known risks, and artifact recommendation.
```
