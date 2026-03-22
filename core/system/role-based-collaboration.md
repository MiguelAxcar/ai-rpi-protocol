purpose: define the human role layer for collaboration; output: role selection, role-aware packaging, handoff routing, and approval boundary defaults; use when: human collaboration target, handoff, approval, or role-aware packaging materially matter.

# Role-based collaboration

AI-RPI needs a human collaboration layer, not just an agent runtime layer.

Core distinction:
- **Mode** = what the user wants
- **Depth** = how much ceremony is needed
- **Persona** = how the assistant communicates and what it emphasizes
- **Human role** = which human viewpoint the work is being shaped for right now, or which human should receive it next

Human role is separate from Mode / Depth / Persona.

Role affects:
- what explanation style will be most useful
- which artifacts are likely to help
- which handoff target should receive the result
- which approval boundary is being approached
- what "done for now" means

Role does not:
- change the public Research -> Plan -> Implement spine
- replace Persona
- create tool permissions or org-chart logic
- force extra ceremony on small work

One person can hold multiple roles. In a small team, the founder may also be the PM, engineer, or reviewer. AI-RPI should treat roles as collaboration targets, not job titles.

## Core role set

| Role | Primary need | Default packaging | Likely "done for now" signal |
|------|--------------|-------------------|-------------------------------|
| **engineer** | implement, debug, verify, and keep momentum | concise diff summary, validation evidence, exact next steps | the work is clear enough to code, test, or merge from an execution standpoint |
| **reviewer** | inspect risk, correctness, and evidence quality | review package, reviewer focus, acceptance mapping, confidence and gaps | a merge or risk decision can be made efficiently |
| **tech lead** | judge architecture, boundaries, and long-term fit | tech spec or ADR when needed, boundary summary, trade-offs, diagram | architecture direction is clear enough to approve or redirect |
| **PM-founder** | judge user outcome, scope, sequencing, and cuts | user story or PRD when needed, scope summary, launch risks, options | product direction or scope choice is clear enough to approve |
| **stakeholder** | understand outcome, impact, and status without deep code detail | plain-language handoff note, demo notes, validation summary in business terms | the business outcome is understandable and decision-ready |

## Role selection

Start simple:
- infer the primary role from the ask when obvious
- if unclear, default to `engineer`
- identify the likely next role when the work will be handed off

Common signals:
- code, debugging, implementation details -> `engineer`
- review, audit, merge-readiness, risk inspection -> `reviewer`
- boundaries, interfaces, long-term structure, pattern choice -> `tech lead`
- user value, roadmap, MVP cuts, priority, delivery trade-offs -> `PM-founder`
- status update, demo, rollout summary, non-technical explanation -> `stakeholder`

It is normal for a task to move across roles:
- `PM-founder` -> `engineer` -> `reviewer`
- `tech lead` -> `engineer` -> `reviewer`
- `engineer` -> `stakeholder`

This is routing, not a new phase system.

## Role-aware packaging

When packaging work, tune the output to the role that needs to act next.

| Role | Emphasize | Likely useful artifacts | Likely next handoff |
|------|-----------|-------------------------|---------------------|
| **engineer** | changed files, commands, risks to implementation, exact next step | brief plan, validation summary, PR description | reviewer or stakeholder |
| **reviewer** | acceptance mapping, confidence, validation gaps, reviewer focus | review package, validation summary, PR description | engineer or tech lead |
| **tech lead** | boundary impact, trade-offs, pattern fit, rollout posture | tech spec, ADR, diagram, review package | engineer or reviewer |
| **PM-founder** | user outcome, scope edges, milestone impact, cuts and options | user story, PRD, concise handoff note | engineer or stakeholder |
| **stakeholder** | outcome, impact, status, open risks in plain language | handoff note, demo notes, plain-language validation summary | PM-founder or engineer |

## Approval boundaries

AI-RPI should make approval boundaries explicit when work is being prepared for a decision.

Approval boundaries are collaboration defaults, not hard permissions.

Rules:
- `engineer` approval usually covers implementation approach and bounded execution inside current patterns and constraints
- `reviewer` approval usually covers merge-readiness, evidence quality, and unresolved risk visibility
- `tech lead` approval usually covers boundary changes, new abstractions, pattern departures, and cross-cutting rollout posture
- `PM-founder` approval usually covers scope, user-visible trade-offs, sequencing, and acceptable cuts
- `stakeholder` approval usually covers whether the outcome is understandable, communicable, and aligned with the business ask

When multiple boundaries apply, surface the highest-leverage next approver instead of asking everyone at once.

## Handoff routing

When packaging or asking for a decision, route to the role that owns the next meaningful question.

- "Should we build this, cut scope, or change priority?" -> `PM-founder`
- "Is this architecture direction acceptable?" -> `tech lead`
- "Is this safe and reviewable to merge?" -> `reviewer`
- "What should be implemented next?" -> `engineer`
- "How do we explain or demo this outcome?" -> `stakeholder`

Handoff outputs should name:
- who the package is for
- what decision is being asked of them
- what evidence or artifact is attached
- what remains uncertain

## Anti-overengineering rules

- do not invent a matrix of twenty roles
- do not treat roles as access control
- do not force a role change when one person clearly owns multiple concerns
- do not generate heavier artifacts just because a role exists
- do use role-aware packaging when it saves human time or clarifies the next decision

## Practical examples

- **Founder asking for a launch update** -> treat this as `stakeholder` unless they are actively shaping scope; give a plain-language summary, current status, visible risk, and recommended next decision.
- **Engineer fixing a bug** -> treat this as `engineer`; keep the output implementation-first with changed files, validation evidence, and the fastest useful next step.
- **Reviewer checking a PR before merge** -> treat this as `reviewer`; package findings, confidence, validation gaps, and reviewer focus instead of a raw diff recap.
- **Tech lead evaluating a boundary change** -> treat this as `tech lead`; surface trade-offs, interface impact, and whether an ADR, tech spec, or diagram is justified.
- **PM-founder shaping an MVP cut** -> treat this as `PM-founder`; frame the decision around user outcome, scope edges, and acceptable cuts before implementation detail.
- **Stakeholder asking what changed for users** -> treat this as `stakeholder`; summarize outcome, business impact, rollout implications, and any open user-facing risk without burying them in code detail.