purpose: define Plan phase contract; output: spec/PRD scaled to protocol level; use when: Plan phase in any level that executes phases.

# Phase: Plan

Purpose: Shape the right solution, challenge it, and select the lightest shaping artifact that still creates clarity.

---

## Internal sub-phases

Planning contains:

- **Shape** — choose the right solution shape for the ask
- **Challenge** — expose weak assumptions, bad ideas, and hidden costs
- **Sequence** — select the lightest useful shaping artifact and order the work proportionally

## Shaping artifact ladder

Shaping artifacts are proportional. Choose the lightest one that still creates clarity.

### No doc

Use when the task is obvious, low-risk, and a document would add no value.

### Brief plan

Use when a short sequence and a few risks are enough.

```
Goal: <one sentence>
Approach: <one short paragraph>
Steps:
1. <step>
2. <step>
Risks:
- <risk>: <mitigation>
```

### User story

Use when the main need is clarifying user intent or feature framing.

```
User story: As a <who>, I want <what>, so that <why>.
Success criteria:
- <criterion>
- <criterion>
```

### Tech spec

Use when the work is primarily technical design, integration, migration, or systems behavior.

### PRD

Use when the work is primarily product-facing or needs explicit outcome framing.

### PRD + tech spec

Use when both product intent and technical delivery need reviewable artifacts.

### ADR / decision memo

Use when the main need is recording a consequential architectural or policy decision rather than a full execution plan.

---

## Invariant rules

- No implementation without enough planning for the risk. Not every task needs a document, but every non-trivial execution task needs deliberate shaping.
- Plan must be grounded in Research findings. Do not invent constraints or ignore discovered ones.
- Challenge the user's preferred approach if Research findings suggest it's suboptimal.
- Every plan must include at least one risk, even for simple changes.
- Every non-trivial plan must define what later validation needs to prove, not just what implementation should change.
- If a heavier shaping artifact would materially reduce ambiguity, explain why and ask before generating it unless the user already asked for it.
- Surface artifact drift when the request, chosen shaping artifact, and likely delivery outputs no longer line up.
- "When appropriate" items (edge cases, failure modes, migration) — use judgment, but err toward including them. If you skip one, note why.
- One option is not a plan. At lite and full levels, present at least two genuinely distinct approaches.

---

## Checklist

Before presenting the plan, verify:

- [ ] Plan is grounded in Research findings
- [ ] Artifact choice is proportional to the request
- [ ] Heavier artifact recommendations are justified before generation
- [ ] Architecture decision is explicit (even if simple)
- [ ] Tasks are ordered and specific enough to implement without guessing
- [ ] Edge cases identified (when appropriate)
- [ ] Failure modes identified (when appropriate)
- [ ] Migration risks assessed (when appropriate)
- [ ] At least one risk surfaced with mitigation
- [ ] Acceptance mapping or acceptance criteria are explicit enough to validate later
- [ ] Trade-offs exposed to the user
- [ ] At least two approaches presented (lite and full levels)

---

## Risk thinking (lite and full levels)

Every plan at lite or full level must include explicit risk analysis.

- **What could go wrong** — specific scenarios, not generic "tests might fail"
- **Blast radius** — if this breaks, what else breaks?
- **Detection** — how would you know it broke?
- **Mitigation** — what reduces the risk before it happens?
- **Rollback** — can you undo this? How?

At lite level, keep this to 2-3 key risks.
At full level, produce a risk register table with likelihood and impact ratings.

---

## Memory (before the gate)

Write to memory if the protocol level requires it:
- `/ai-rpi-protocol/memory/plans/{task}-plan.md` — the plan artifact (use template at `/ai-rpi-protocol/templates/plan-output-template.md`)
- `/ai-rpi-protocol/memory/decisions.md` — decisions and rationale
- `/ai-rpi-protocol/memory/session-state.md` — current phase and task status

If a shaping artifact should be shareable beyond the session, prefer `{workspace_root}/artifacts/shaping/`.

Memory is silent — update before presenting the gate.

---

## Shaping artifacts beyond the brief plan

Load and follow: `/ai-rpi-protocol/core/phases/planning-prd-techspec-guidance.md`

When appropriate (Mode, Depth, and solution size warrant it):

1. **Choose template** — PRD vs Tech Spec by work type; micro / condensed / full by solution size.
2. **Recommend before generating** — If PRD, Tech Spec, PRD + Tech Spec, or ADR would help, explain why and ask before generating unless the user already asked for it.
3. **Write to shaping artifact directory** — Prefer `{workspace_root}/artifacts/shaping/` for shareable, version-controllable shaping artifacts; fallback `memory/plans/` for session-only.
3. **Multi-PRD automation** — If the plan yields 2+ independent deliverables:
   - Write one shaping artifact per deliverable under `artifacts/shaping/`.
   - Suggest: *"I can implement each via a subagent and run a code review per implementation. Proceed that way?"*
   - If user confirms: spawn Implement subagent per spec → spawn Code Review subagent per implementation → verify steps.

Templates: `prd-template-{micro|condensed|full}.md`, `tech-spec-template-{condensed|full}.md`.

---

## Code review and multi-issue tasks

**Note:** For standalone "review this code" requests, prefer the **Code Review skill** (`/ai-rpi-protocol/skills/code-review.md`). It owns the deeper multi-lens review workflow. Use `/ai-rpi-protocol/templates/restate-code-review-request.md` only when the review target is ambiguous.

When Research produces a list of independent issues (code reviews, audits, quality assessments) as part of a broader RPI task, Planning means **advise per issue** instead of picking one approach for the whole task.

For each issue found in Research:
- Why it's bad (concrete impact)
- Options to fix it (genuinely distinct, per anti-anchoring rules)
- Trade-offs of each option
- Suggested approach with reasoning

Use the per-issue format from `/ai-rpi-protocol/templates/code-review-output-template.md`.

The gate for review-style tasks: "Which issues do you want to fix? Want to adjust any suggested approaches?"

---

## Delegation guidance

Planning can stay in the main thread or use a focused subagent when an independent challenge or specialist review would materially improve the plan.

Typical Planning subagents:
- `challenger` when assumptions, trade-offs, or scope need pressure
- `architecture-reviewer` when boundaries, interfaces, or long-term fit matter
- `codebase-mapper` when option feasibility still depends on unclear repo structure
- `standards-discovery` when conventions should shape the chosen plan
- `documentation-researcher` when external docs shape the plan

If delegating:
- pass Research findings, constraints, desired artifact depth, and this phase file
- ask for a narrow planning output that unlocks a specific decision
- keep the main agent responsible for synthesis and the gate

---

## Challenge and friction

Planning is where alternatives and trade-offs must be explicit.

- If there is only one approach, find at least one alternative. One option is not a plan — it's a recommendation disguised as a choice.
- If the user's preferred approach has downsides, state them clearly. Do not bury risks in bullet points.
- If a simpler approach exists, surface it even if the user asked for something complex.
- Expose hidden costs: maintenance burden, testing complexity, operational overhead, future migration difficulty.
- If the plan requires changes that conflict with existing architecture, flag the conflict and explain the trade-off.

Format: `"AI-RPI flagging <what> - <why it matters>."`

---

## Gate

"Does this plan give enough clarity? Should we stop here, revise it, or continue into implementation?"

Do not proceed without explicit confirmation.
