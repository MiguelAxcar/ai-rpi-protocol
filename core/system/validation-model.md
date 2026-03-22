purpose: define validation as the protocol's proving model; output: validation layers, review distinction, confidence rules, uncertainty handling, acceptance mapping, and escalation triggers; use when: implementation, review, confidence, done-ness, or guardrail-sensitive proof materially matter.

# Validation model

Validation is the main public proving term in AI-RPI.

Validation answers: **why should anyone trust that this work is actually done?**

Review is related, but different.

Core distinction:
- **Validation** = the total evidence-backed process for proving the result is fit for purpose
- **Review** = a judgment pass, usually through one or more lenses, used when validation needs stronger scrutiny

Short version:
- validation is the umbrella
- review is one possible layer inside validation
- implementation is not proof
- passing tests is not automatically proof
- a small change is not automatically low impact

This distinction is intentional. Do not blur it.

## What validation includes

Validation is multi-layered and proportional.

Possible validation layers:
1. **Execution checks** — lint, typecheck, build, tests, static checks, targeted scripts
2. **Behavior checks** — prove the change behaves as intended, not just that it compiles
3. **Acceptance mapping** — compare the result against the request, user story, plan, PRD, tech spec, or explicit acceptance criteria
4. **Uncertainty reporting** — state what remains unknown, untested, or only partially verified
5. **Review lenses** — add human-like or specialist judgment when simple checks are not enough
6. **Reviewer focus** — tell the next reviewer exactly where scrutiny should go

Not every task needs every layer.

Rules:
- use the fewest useful layers first
- widen validation when risk, user impact, criticality, or uncertainty justify it
- do not confuse one passed check with full validation
- do not claim done without saying what evidence actually exists

## Validation vs review

Validation is broader than review.

Validation can exist without a formal review pass:
- trivial mechanical rename with passing local checks and obvious acceptance match
- narrow config tweak with one targeted verification step

Review becomes necessary when judgment matters more than raw checks alone.

Review is for:
- correctness questions not settled by tests alone
- maintainability and readability
- architecture fit and boundary quality
- product fit and workflow fit
- performance implications
- security implications
- reviewability and handoff quality

Review should never be treated as a ceremonial separate finish step.
It is one widening layer inside validation.

## Review lenses

AI-RPI can widen review through one or more lenses:
- correctness
- maintainability
- architecture fit
- product fit
- performance
- security
- reviewability and handoff quality

Rules:
- keep review proportional
- prefer the fewest useful lenses
- use specialist reviewers only when they add signal
- state which lenses were actually applied

## Acceptance mapping

Acceptance mapping is a first-class part of validation.

Acceptance mapping compares the work across the chain that justified it:
- user request
- inferred or confirmed user story
- plan
- PRD or tech spec when present
- implementation
- validation evidence

It answers:
- what was requested?
- what was planned?
- what actually changed?
- what evidence proves the change meets the intended outcome?
- where does the mapping remain partial or uncertain?

Acceptance mapping should be explicit when:
- the task crosses multiple files or modules
- the task is user-facing
- the task is high-risk or hard to reverse
- the implementation could appear correct while still missing intent
- the work is being packaged for review or handoff

Lean format:

| Anchor | Current statement | Evidence | Status |
|--------|-------------------|----------|--------|
| Request | <what the user asked for> | <files/tests/manual proof> | matched / partial / unmet |
| Plan or spec | <what was approved> | <diff/tests/checks> | matched / partial / unmet |
| Outcome | <actual behavior/result> | <behavior proof> | verified / likely / unverified |

## Confidence signaling

Confidence must be evidence-based, not tone-based.

Use explicit confidence levels when technical claims or completion claims matter:
- **Low confidence** — limited evidence, significant uncertainty, important gaps remain
- **Medium confidence** — some direct evidence exists, but coverage is incomplete or key assumptions remain
- **High confidence** — direct evidence covers the important acceptance path and remaining uncertainty is small

Confidence must be about the claim being made, not about how persuasive the wording sounds.

Examples:
- high confidence in compilation, medium confidence in runtime behavior
- high confidence in a narrow fix, low confidence in hidden blast radius
- medium confidence overall because acceptance mapping is only partial

Never use confidence to hide missing evidence.

## Uncertainty handling

Uncertainty must be visible.

State uncertainty explicitly when:
- a path was not tested
- behavior was inferred from code but not executed
- acceptance criteria were ambiguous
- surrounding systems or integrations were not available
- a risky assumption remains unresolved

Useful uncertainty outputs:
- what remains unknown
- what was not validated
- what should be reviewed next
- what evidence would raise confidence

## Scaling validation

Validation scales with more than Depth.

Depth matters, but widen validation based on:
- **criticality** — auth, permissions, payments, migrations, data integrity, production safety, compliance, irreversible actions
- **user impact** — how many users, workflows, or business outcomes could be affected
- **uncertainty** — how much is still inferred, ambiguous, or untested
- **blast radius** — how many systems, modules, contracts, or teams are exposed

Strong rule:
- **small change != low impact**

Examples:
- a one-line permission check can require full validation
- a tiny config change can need strong rollout scrutiny
- a narrow migration script can be higher criticality than a 20-file refactor

## Criticality triggers

Escalate validation when any of these appear:
- auth, permissions, identity, secrets, encryption, or trust boundaries
- payments, billing, quotas, or money movement
- migrations, schema changes, or irreversible writes
- compliance, PII, legal, or safety-sensitive behavior
- concurrency, caching correctness, background jobs, or distributed coordination
- user-facing flows with high operational or reputational impact
- changes with unclear rollback or detection paths

## Validation and deterministic guardrails

Validation and guardrails are related, but they are not the same thing.

- **Validation** answers whether the evidence is strong enough to trust the result.
- **Guardrails** answer whether the assistant is allowed to proceed autonomously, must confirm, must escalate, or must stop automatic execution.

Rules:
- stronger validation does not replace confirmation when a critical surface requires explicit user control
- passing checks does not cancel a destructive-action guardrail
- partial validation on a critical surface should raise the guardrail posture, not hide under a confident summary
- weak evidence should narrow claims and can require confirmation or escalation before proceeding

Examples:
- a small checkout flag change with only partial behavior proof may require **confirm critical** plus stronger review
- a migration with a solid plan can still be **never automatic** for execution if the action is destructive or irreversible
- a cross-boundary interface change with passing tests can still trigger stronger review because validation is local but impact is broader

## Review triggers

Widen into review lenses when:
- checks passed but intent match is still uncertain
- the design may fit poorly with existing boundaries
- the change is easy to misunderstand or hard to review from the diff alone
- critical paths have thin or indirect test coverage
- the blast radius is larger than the diff suggests
- risk is concentrated in a specialist domain such as security or performance
- the human reviewer needs focused guidance instead of a raw validation dump

## Reviewer focus

Validation should help the next reviewer spend attention where it matters.

Reviewer focus should say:
- what area deserves the most scrutiny
- which acceptance anchors are still weakest
- which uncertainty matters most
- which lens or specialist review would add the most signal

Good examples:
- `Reviewer focus: verify the permission boundary in the new fallback path; tests cover the happy path but not role downgrades.`
- `Reviewer focus: acceptance mapping is strong for the API contract but weaker for background retry behavior.`

## Human approvals and handoffs

Validation should help the next human make the next decision, not just inspect raw evidence.

When work is being packaged for review, approval, or transfer:
- identify the likely next human role
- state what decision that role is being asked to make
- tailor the summary, focus, and artifact recommendation to that role
- surface the approval boundary that is actually in play

Common examples:
- `reviewer` -> merge-readiness, validation gaps, and where scrutiny should go first
- `tech lead` -> boundary fit, pattern choice, and whether the direction should be approved or redirected
- `PM-founder` -> scope choice, user impact, and acceptable cuts or sequencing
- `stakeholder` -> business outcome, rollout understanding, and current status in plain language

## Depth guidance

### Minimal

- prefer execution checks plus one clear behavior check
- skip review unless impact or uncertainty makes it necessary
- still state uncertainty if evidence is thin

### Balanced

- combine checks, behavior validation, and light acceptance mapping
- add one or two review lenses when risk or ambiguity justifies it
- include reviewer focus when packaging would save time

### Full

- validation should be reviewer-grade
- acceptance mapping should be explicit
- confidence should be stated clearly
- uncertainty should be visible and actionable
- multiple review lenses or specialists are normal when criticality justifies them

## Output expectations

When validation materially matters, outputs should make these visible:
- validation evidence
- confidence level
- uncertainty or remaining gaps
- acceptance mapping status
- reviewer focus
- likely handoff role or approval boundary when the work is being packaged for a decision

Validation is what lets AI-RPI say a result is reviewable, trustworthy, and ready for the next decision.