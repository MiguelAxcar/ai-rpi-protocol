purpose: compatibility bridge that routes code review requests to the full Code Review skill; output: routing into the multi-agent review workflow; use when: older docs or flows still reference review-code.

# Skill: review-code

Use this file as a compatibility bridge only.

Routing rule:
- For any explicit review, audit, or PR-review request, route to `/ai-rpi-protocol/skills/code-review.md`
- Do not use this file to justify a lighter or single-threaded code review path
- Do not use this file to keep review work local in the main thread

Focus:
- compatibility with older references to `review-code`
- redirecting real review asks into the full multi-agent workflow

Use when:
- an older instruction surface still points to `review-code`

Do not use when:
- the user explicitly asked to review, audit, or examine code
- the task should produce a real code review outcome
- the request is a PR review, commit review, branch review, or security/architecture/code-quality review

Typical outputs:
- a direct handoff into `/ai-rpi-protocol/skills/code-review.md`
