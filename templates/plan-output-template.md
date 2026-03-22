purpose: plan artifact template; output: structured plan .md; use when: Planning phase output.

# Plan Template

**Use this template when writing a plan to memory.** Adapt sections to the task — skip what's not relevant, add what's missing.

---

# Plan: [Task/Feature Name]

**Date:** [Date]
**Depth:** [minimal/balanced/full]
**Recommended shaping artifact:** [no doc / brief plan / user story / PRD / tech spec / PRD + tech spec / ADR]

## Goal

[What we're trying to achieve and why]

## Options

### Option 1: [Approach Name]

[How this approach works]

- Pros: [benefits]
- Cons: [drawbacks]
- Trade-offs: [what is gained vs lost]
- Effort: [Low/Medium/High]

### Option 2: [Alternative Approach]

[How this approach works]

- Pros: [benefits]
- Cons: [drawbacks]
- Trade-offs: [what is gained vs lost]
- Effort: [Low/Medium/High]

## Recommendation

**Chosen:** Option [X] — [why this one]

**Why not the others:** [brief reasoning]

**Artifact choice:** [why this shaping artifact is the lightest one that preserves clarity]

**Likely delivery artifacts:** [PR description / review package / handoff note / validation summary / diagram / QA checklist / none]

## Implementation steps

- [ ] [Step] — files: [which files], why: [reasoning]
- [ ] [Step] — files: [which files], why: [reasoning]
- [ ] [Step] — files: [which files], why: [reasoning]

## Files to touch

- Create: [new files if any]
- Modify: [existing files]
- Dependencies: [new packages if any]

## Risks

- [Risk 1] — severity: [L/M/H], mitigation: [how to handle]
- [Risk 2] — severity: [L/M/H], mitigation: [how to handle]

## Acceptance mapping

- Request: [what must be true to satisfy the user ask]
- Plan/spec: [what the approved plan commits to]
- Validation anchors: [what evidence should prove the result]

## Validation plan

- Checks: [tests/build/lint/scripts]
- Behavior proof: [manual or automated proof of intended behavior]
- Uncertainty to resolve: [what is still ambiguous or risky]
- Reviewer focus: [where human review should concentrate]

## Drift watch

- Request to artifact fit: [what could drift]
- Artifact to implementation fit: [what could drift]
- Delivery risks: [what downstream artifact may be needed if scope changes]

## Testing

- [What to test and how]
- [Edge cases to cover]

## Done when

- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] Tests pass
