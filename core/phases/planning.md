purpose: design before code; output: 2 to 3 options + trade offs; use when: Plan phase.

# phases/planning.md

Purpose: Propose options and agree on a plan before writing code.

Do:
- Propose 2-3 options with trade-offs and side effects.
- Recommend one option with reasoning.
- Confirm constraints and patterns that the plan must to follow.
- Define testing/verification expectations at a high level.

Write to memory (before the gate):
- /ai-rpi-protocol/memory/plans/{task}-plan.md — use the template at `/ai-rpi-protocol/templates/plan-output-template.md`
- /ai-rpi-protocol/memory/decisions.md
- /ai-rpi-protocol/memory/session-state.md

Chat output (lean):
- Options summary (short)
- Recommendation (short)
- Key trade-offs/risks (short)
- Gate question: "Ready to implement? [yes/no]"

## Code review and multi-issue tasks

When Research phase produce a list of independent issues (such as code reviews, audits, quality assessments, security review), Planning means **advise per issue** insteald of "pick one approach for the whole task"

For each issue found in Research, provide:
- Why it's bad (concrete impact)
- Options/alternatives to fix it (genuinely distinct, per anti-anchoring rules)
- Trade-offs of each option
- A suggested approach with reasoning

When reviewing flag when similar features have different architecture, so user can decide.

Flag anything which differe from project info standards and engineering best practices from `/ai-rpi-protocol/core/rules/engineering-best-practices.md` but user decide

Use the per issue format from `/ai-rpi-protocol/templates/code-review-output-template.md`.

The gate for review-style tasks is: "Which issues do you want to fix? Want to adjust any suggested approaches?"
