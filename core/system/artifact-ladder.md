purpose: define the artifact ladder as AI-RPI's proportional artifact model; output: shaping vs delivery ladders, recommendation behavior, relationships, drift rules, and naming guidance; use when: planning, packaging, or artifact generation materially matter.

# Artifact ladder

AI-RPI produces the right artifacts for the job, from lightweight shaping to reviewable handoff.

The artifact ladder is a visible product feature, not a hidden implementation detail.

It exists to keep artifacts proportional:
- preserve clarity without defaulting to heavyweight documentation
- bridge shaping work and reviewable delivery
- make recommendations when artifacts add real value
- keep the engineer in control

Core rules:
- **Prefer the lightest artifact that preserves clarity.**
- **When a heavier artifact may provide meaningful value, briefly explain why and ask before generating it.**
- avoid artifact sprawl
- avoid documentation theater
- use artifacts to improve clarity, reviewability, and delivery, not to create noise

## Core distinction

### Shaping artifacts

Shaping artifacts help define, clarify, align, or sequence the work before or during implementation.

They answer questions like:
- what are we actually building?
- what constraints shape the work?
- which trade-offs were chosen?
- what should later validation prove?

### Delivery artifacts

Delivery artifacts help review, validate, communicate, or hand off the work after or around implementation.

They answer questions like:
- what changed?
- how was it validated?
- where should reviewers focus?
- what does the next engineer or stakeholder need to know?

This split is deliberate. It keeps AI-RPI from treating all documents as the same kind of output.

## Shaping artifact ladder

Not every task should create a shaping artifact.

The core shaping artifact ladder is:
1. **no doc**
2. **brief plan**
3. **user story**
4. **PRD**
5. **tech spec**
6. **PRD + tech spec**
7. **ADR / decision memo**

### Core shaping guidance

| Artifact | Use when | Typical weight |
|----------|----------|----------------|
| no doc | the task is obvious, bounded, and a document would add no value | lowest |
| brief plan | a short sequence, a few risks, and basic alignment are enough | light |
| user story | user intent or workflow framing needs sharper definition | light |
| PRD | product-facing outcomes, scope, or success criteria need durable clarity | medium |
| tech spec | technical design, interfaces, migration, or architecture need durable clarity | medium |
| PRD + tech spec | both product intent and technical design are broad, ambiguous, or high-risk | heavy |
| ADR / decision memo | a meaningful architectural or boundary decision deserves explicit rationale | focused heavy |

Rules:
- prefer the lightest artifact that preserves clarity
- user story may be inferred and proposed when useful, especially for Feature and Build
- PRD and tech spec may both be recommended when the work is broad enough or ambiguous enough
- ADR / decision memo is for durable decisions, not for routine planning noise

## Extended optional shaping artifacts

AI-RPI may also recommend extended shaping artifacts when the request clearly benefits from them.

These are recommendation-driven, not default first-class outputs:
- stakeholder brief
- discovery brief
- implementation plan
- rollout plan
- migration plan
- validation plan
- test strategy

Examples:
- stakeholder brief for presentation-oriented or leadership-facing work
- rollout plan for risky rollout or operational sequencing concerns
- migration plan for data or contract transitions
- validation plan or test strategy when acceptance risk is high and validation needs explicit shaping

## Delivery artifact ladder

Delivery artifacts should also stay proportional.

The core delivery artifact ladder is:
- **PR description**
- **review package**
- **handoff note**
- **validation summary**
- **diagram**

### Core delivery guidance

| Artifact | Use when | Typical leverage |
|----------|----------|------------------|
| PR description | the result will move through a PR-centric workflow or needs a concise reviewer summary | high, often light |
| review package | reviewers need a stronger bundle of context, focus, trade-offs, and validation evidence | medium to high |
| handoff note | ownership is moving to another engineer, team, or future session | medium |
| validation summary | confidence, evidence, uncertainty, and acceptance mapping need to be explicit | medium to high |
| diagram | visual reviewability or stakeholder clarity beats prose | selective |

Rules:
- delivery artifacts should make human review easier
- PR-centric workflows are first-class in AI-RPI
- diagrams are optional delivery artifacts, not a default requirement

## Extended optional delivery artifacts

AI-RPI may also recommend extended delivery artifacts when the work clearly benefits from them.

These remain optional and recommendation-driven:
- QA checklist
- reviewer focus note
- release note draft
- rollback note
- stakeholder summary
- demo script
- testing note
- migration handoff
- launch checklist

Guidance:
- **QA checklist** can be recommended more aggressively than many other optional delivery artifacts when it clearly improves handoff or review quality
- none of these should become mandatory default noise

## Recommendation before generation

Recommendation behavior is part of the product model.

AI-RPI should:
- recommend an artifact when it is likely to add value
- briefly explain why
- ask before generating heavier artifacts when appropriate
- keep the user in control
- avoid creating docs just because they exist in the system

Good examples:
- `AI-RPI-Protocol detected that a tech spec may reduce ambiguity here and improve implementation quality. Do you want me to generate it?`
- `AI-RPI-Protocol detected that a stakeholder brief may help you communicate this clearly in a presentation. Do you want me to generate it?`
- `AI-RPI-Protocol detected that a QA checklist may improve handoff quality for this change. Do you want me to generate it?`

Practical rule of thumb:
- brief plan and user story can often be proposed inline with low noise
- PRD, tech spec, PRD + tech spec, ADR / decision memo, and most extended artifacts usually deserve explicit confirmation before generation unless the user already asked for them
- PR description and light validation summary can often be recommended near completion
- review package, diagram, QA checklist, or stakeholder-facing artifacts should usually be recommended with a short reason before generation

## Artifact relationships

Artifacts should feel connected, not like disconnected documents.

Useful relationship map:
- request -> user story
- request -> brief plan
- user story -> PRD
- PRD -> tech spec
- PRD + tech spec -> implementation
- plan/spec/story -> validation
- implementation -> PR description / review package / handoff note / validation summary
- delivery artifacts -> human review / stakeholder communication / handoff

## Artifact relationship map

```text
request
  -> no doc | brief plan | user story
  -> PRD
  -> tech spec
  -> PRD + tech spec
  -> ADR / decision memo

user story -> PRD
PRD -> tech spec
PRD + tech spec -> implementation
plan/spec/story -> validation

implementation
  -> PR description
  -> review package
  -> handoff note
  -> validation summary
  -> diagram

delivery artifacts -> review, handoff, stakeholder communication, launch support
```

## Artifact drift

Artifact drift is a real feature, not bookkeeping noise.

AI-RPI should detect and surface practical drift between:
- request
- user story
- brief plan
- PRD
- tech spec
- implementation
- validation results
- delivery artifacts

Examples of drift:
- implementation no longer matches the story
- plan changed but the spec was not updated
- PR description no longer reflects what changed
- validation summary does not line up with what was built
- handoff note omits important trade-offs or uncertainty

Rules:
- drift should be surfaced, not hidden
- drift should not automatically create more documentation
- drift handling should stay practical: either update the artifact, flag the mismatch, or recommend the lightest correction that preserves clarity

### Drift rule set

1. Check major shaping artifacts against the current request and chosen direction before execution hardens.
2. Check implementation against the approved shaping artifact when the work is non-trivial.
3. Check validation summary against actual validation evidence.
4. Check PR description, review package, and handoff note against what actually changed.
5. If drift is minor, flag it inline.
6. If drift materially affects review, handoff, or acceptance clarity, recommend updating the relevant artifact.
7. Do not create a new artifact just to say drift exists unless that new artifact clearly adds leverage.

## Diagram behavior

Diagrams are optional delivery artifacts.

Recommend them when they improve reviewability or communication, especially for:
- cross-module work
- architecture-heavy changes
- stakeholder presentations
- onboarding or handoff situations
- complex flows that are easier to review visually

Do not recommend diagrams by default for all meaningful work.

## PR-centric behavior

AI-RPI can end in PR-oriented outputs such as:
- PR description
- reviewer focus
- validation summary
- review package
- handoff package

This keeps the protocol aligned with modern PR-centric workflows rather than treating implementation as the end of the story.

## Directory and naming guidance

Recommended artifact directory structure:

```text
artifacts/
  shaping/
  delivery/
```

Guidance:
- keep folders simple
- keep names descriptive
- optimize for sorting, discovery, and maintainability
- use dated filenames for history and scanability

Recommended filename style:
- `20260302-user-story-checkout-flag.md`
- `20260302-prd-checkout-retry-flow.md`
- `20260302-tech-spec-checkout-retry-flow.md`
- `20260302-adr-checkout-boundary.md`
- `20260302-pr-description-checkout-retry-flow.md`
- `20260302-review-package-checkout-retry-flow.md`
- `20260302-validation-summary-checkout-retry-flow.md`
- `20260302-handoff-checkout-retry-flow.md`
- `20260302-diagram-checkout-retry-flow.md`

Compatibility note:
- `plans/` can remain as a legacy or compatibility location for older plan-only workflows
- `artifacts/shaping/` and `artifacts/delivery/` are the recommended shareable artifact locations going forward
- memory artifacts remain valid for session-only state and compaction

## Mode x Depth x artifact matrix

| Mode | Minimal | Balanced | Full |
|------|---------|----------|------|
| Explore | usually no doc; brief plan only if it prevents ambiguity | brief plan or user story when shaping matters; handoff note only if useful | brief plan, user story, or discovery brief when the exploration must survive review or coordination |
| Discuss | brief plan or user story | brief plan, user story, tech spec, or PRD when trade-offs need durable clarity | PRD, tech spec, PRD + tech spec, or ADR / decision memo when the decision is broad, risky, or durable |
| Review | no shaping artifact by default; light PR description or reviewer focus when useful | review package or validation summary when findings need structure | review package, validation summary, QA checklist, or diagram when reviewability and handoff need stronger support |
| Patch | often no doc; PR description can still help | brief plan when the patch has hidden trade-offs; PR description or validation summary when reviewability benefits | brief plan or tech spec only if the patch hides real complexity; review package or handoff note when impact is larger than the diff |
| Feature | user story may be inferred; no doc only for very small additive work | user story, PRD, or tech spec depending on ambiguity; PR description and validation summary are common delivery outputs | PRD + tech spec often justified for broad or ambiguous work; review package, handoff note, validation summary, and diagram when reviewability needs it |
| Build | usually no shaping artifact unless tightly bounded | brief plan, tech spec, migration plan, or rollout plan when needed; PR description or handoff note on delivery | tech spec, PRD + tech spec, ADR / decision memo, rollout or migration plan when justified; delivery often includes review package, validation summary, QA checklist, and possibly diagram |

## Anti-overengineering guardrails

- Prefer the lightest artifact that preserves clarity.
- Recommend heavier artifacts only when they are likely to provide real value.
- Explain why before generating heavier artifacts.
- Ask the user before generating heavier artifacts when appropriate.
- Avoid artifact sprawl.
- Avoid turning AI-RPI into a documentation factory.
- Use artifacts to improve clarity, reviewability, and delivery - not to create noise.