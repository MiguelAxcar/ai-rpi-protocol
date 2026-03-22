purpose: define adaptive runtime selection; output: mode choice + depth choice; use when: start of request or re-assess.

# Mode and Depth

This file keeps the legacy `modes.md` path, but it now defines the adaptive runtime layer around the public RPI spine.

- **Mode** = what the user wants
- **Depth** = how much ceremony is needed

Goal:
- Keep the default experience proportional.
- Put rigor where the task actually needs it.
- Avoid bureaucracy by default while keeping accountability by default.
- Help engineers generate value and deliver results.
- Be a thoughtful partner, not a passive pleaser.

Mode and Depth are orthogonal to levels, personas, and human roles.
- A **level** controls how much of the protocol is loaded.
- A **persona** changes voice, emphasis, browsing behavior, and output defaults.
- **Mode** changes what kind of outcome the user is asking for.
- **Depth** changes how much evidence, challenge, planning, validation, and packaging the loop produces.
- A **human role** changes which human viewpoint the work is being shaped for, the likely handoff target, and the approval boundary that matters next.

Operational units are selected on top of this layer:
- skills are reusable workflows
- subagents are specialist delegated workers with fresh context

Role-based collaboration sits beside this runtime layer. It should influence packaging, explanation style, and handoff routing without changing the public RPI spine.

Load `/ai-rpi-protocol/core/system/role-based-collaboration.md` when collaboration target, handoff routing, approval boundaries, or role-aware packaging materially matter.

Mode strongly influences which skills and subagents are likely to help, but it should not blindly preload them.

## Public modes

Use these public modes:

- **Explore** — explain, trace, gather evidence, understand, feasibility-check
- **Discuss** — shape direction, challenge assumptions, compare trade-offs
- **Review** — inspect correctness, quality, validation, and reviewer risk
- **Patch** — make a targeted, bounded change
- **Feature** — add or expand a meaningful capability
- **Build** — carry larger execution work across multiple steps or systems

Internal note:
- `Diagnose` is an internal subtype of **Explore**
- Do not make `Diagnose` a public first-class mode

Patch vs Feature guidance:
- Small asks such as label changes, copy tweaks, narrow validation tweaks, tiny config changes, small test fixes, and bounded UI tweaks usually land as **Patch**
- Meaningful capability additions, new flows, new permission behavior, new endpoints, background work, and user-visible behavior expansion usually land as **Feature**

## Depth selection

The assistant MUST select mode and depth during Research/Inception using these signals:

Primary signals:
- Task risk: prod facing, security, payments, auth, migrations, data integrity.
- Task scope: number of files touched, cross-module changes, refactor breadth.
- Uncertainty: unclear requirements, missing constraints, ambiguous intent.
- Reversibility: easy undo vs one-way door.
- User outcome: Explore, Discuss, Review, Patch, Feature, or Build.

Secondary signals:
- Time pressure hints: “quick”, “fast”, “just do it”, “ship today”.
- Prior failures: repeated rewrites, drift, frequent misunderstandings.
- Context cost: how much should be loaded vs deferred.

Interpretation rules:
- Do not mirror the user's urgency or confidence.
- Classify independently.
- When unsure between two valid classifications, choose the simpler one first and escalate only with evidence.
- Prefer the lightest path that still protects correctness.

## Internal change magnitude heuristic

Use this heuristic internally to support mode and depth selection:

- **tiny** — almost mechanical, local, low-risk
- **bounded** — clearly scoped, limited blast radius
- **meaningful** — real behavior or capability change, moderate impact
- **systemic** — broad design, architecture, or multi-surface impact

This heuristic is internal only. It does not replace Mode or Depth.

If unsure, default to **Patch** or **Explore** on Mode, and **balanced** on Depth.

## Minimal

Use when:
- Small, local, reversible work.
- Low risk.
- The lightest useful loop is enough.

Behavior:
- Load only the smallest relevant context slice.
- Research focuses on classification, local evidence, and whether the loop can stop early.
- Planning may be no doc or a brief plan.
- Packaging is concise but still reviewable.
- Memory is optional.

## Balanced

Use when:
- Default depth for most work.
- Moderate complexity or ambiguity.
- The task benefits from explicit trade-offs but not full ceremony.

Behavior:
- Research maps relevant paths, constraints, and risks.
- Planning challenges assumptions and selects the lightest useful artifact.
- Implementation validates continuously and ends with reviewable work plus proportional delivery artifacts when useful.
- Memory is optional but recommended if the task is likely to span turns.

## Full

Use when:
- High risk, high ambiguity, or broad blast radius.
- One-way doors, migrations, security-sensitive work, or cross-cutting changes.
- The user explicitly asks for maximum rigor.

Behavior:
- Research is deeper and more skeptical.
- Planning includes stronger trade-off challenge, failure modes, and heavier artifact support when justified.
- Implementation uses tighter slicing, stronger validation, and richer packaging.
- Memory is required.

## Depth escalation and de-escalation

The assistant MUST escalate depth when:
- New information increases risk.
- The blast radius grows.
- The request shifts from explanation or review into execution.

The assistant SHOULD de-escalate depth when:
- The task becomes clearly small and local.
- Research shows that more ceremony would not improve the outcome.

## Escape phrases

User phrases that usually push toward minimal:
- “quick”
- “skip planning”
- “just do it”
- “ignore framework”

User phrases that usually push toward full:
- “be careful”
- “do a full plan”
- “treat this as high risk”
- “include rollback and monitoring”
