purpose: classify user requests; output: which template to use; use when: unclear request type.

# Mode Reference

**Purpose:** Reference guide for classifying user requests into the public AI-RPI Modes. The protocol stays RPI-first while the adaptive layer stays practical and low-noise.

---

## Explore

Use for questions, tracing, evidence gathering, understanding, and feasibility checks.

Examples:
- "Explain how the payment flow works"
- "Trace where this value comes from"
- "Can this repo support multi-tenant auth?"
- "Find out why this is slow"

Internal notes:
- `Diagnose` is an internal subtype of Explore
- Explore can internally branch into explain, trace, diagnose, gather evidence, or feasibility check

Template routing:
- Usually `restate-other-request.md`
- May skip restate for narrow informational asks

---

## Discuss

Use for shaping direction before execution.

Examples:
- "How should we structure this feature?"
- "What are the trade-offs between these two approaches?"
- "Challenge this design before we build it"

Template routing:
- Usually `restate-other-request.md`

---

## Review

Use for audits, code review, validation, and correctness checks.

Examples:
- "Review this PR for security issues"
- "Check if this code follows our patterns"
- "Audit this service for quality risks"

Template routing:
- `/ai-rpi-protocol/skills/code-review.md` for standalone review requests
- `/ai-rpi-protocol/templates/restate-code-review-request.md` only when the review target or scope is ambiguous
- `/ai-rpi-protocol/templates/code-review-output-template.md` for per-issue review guidance during planning

Rule:
- explicit review requests should not be downgraded into a small verification pass

---

## Patch

Use for targeted, bounded changes.

Examples:
- "Fix the payment button not working"
- "Patch this bug without changing the architecture"
- "Clean up this narrow issue"
- "Patch a narrow UI label or validation issue"
- "Fix a small test regression"

Template routing:
- `restate-bugfix-request.md` for bug-driven patches
- `restate-other-request.md` for cleanup or refactor-style patches
- May skip restate for trivial local fixes

Usually lands here:
- label change
- copy tweak
- narrow validation tweak
- tiny config change
- small test fix
- bounded UI tweak

---

## Feature

Use for new capabilities with clear user-facing or workflow-facing intent.

Examples:
- "Add PayPal support on checkout"
- "Build a dashboard for analytics"
- "We need email notifications"
- "Add a new permission flow"
- "Create a new endpoint"

Template routing:
- `restate-feature-request.md`

Usually lands here:
- meaningful capability addition
- meaningful behavior expansion
- new flow
- new permission behavior
- new endpoint
- new background work
- user-visible capability expansion

---

## Build

Use for larger implementation work, technical delivery, migrations, integration work, or multi-step execution.

Examples:
- "Migrate this service to TypeScript"
- "Integrate this library across the pipeline"
- "Build the new API layer"

Template routing:
- `restate-feature-request.md` when the ask is outcome-driven
- `restate-other-request.md` when the ask is technical delivery, migration, refactor, testing, or documentation heavy

---

## Internal tags

These are useful internally, but they are not the public first-class Modes:

- bugfix
- refactor
- explanation
- optimization
- testing
- documentation
- cleanup
- migration
- architecture/design

Map them into Explore, Discuss, Review, Patch, Feature, or Build based on user intent.

---

## Classification tips

1. Use the primary intent, not just the keywords.
2. If the request is ambiguous, ask whether the user wants to explore, discuss, review, patch, define a feature, or build.
3. Combined requests can move through multiple kinds over time. Example: Explore -> Discuss -> Patch.
4. Not every request should travel equally far through RPI. Explore may stop after Research, while Feature and Build often continue.
5. When two classifications are plausible, choose the simpler one first and escalate only with evidence.
