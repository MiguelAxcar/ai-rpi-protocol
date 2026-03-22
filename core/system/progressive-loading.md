purpose: define progressive loading as a first-class product feature; output: layers, triggers, budgets, compaction, guardrail-aware widening, and transparency rules; use when: before widening context beyond entry files.

# Progressive loading

Core principle:
- Load the minimum useful context first. Expand only when the task proves it is necessary.
- AI-RPI should not front-load intelligence. It should progressively unlock it.

Progressive loading is not just a token-saving trick. It is part of the product behavior. The user should be able to understand:
- why the assistant started with a narrow context slice
- what caused it to widen
- when it condensed or handed off state
- which layers are currently active

Progressive loading stays compatible with deterministic guardrails:
- risk, criticality, destructive potential, and uncertainty can justify wider loading or tighter control even when the diff is small
- a guardrail can force a hook, confirmation, or escalation before more context or execution continues

## Layered loading architecture

Always move outward in layers. Do not jump to later layers without a reason.

### Layer 0: base invariants

Always start with the minimum rules that make the run safe and coherent.

Includes:
- `AGENTS.md`
- `skills/index.md`
- selected protocol entry file
- required adapters
- `file-index.md`
- `phases.md`

### Layer 1: persistent project context

Load durable project-scoped context that should shape behavior on every interaction.

Includes when present:
- `/ai-rpi-protocol_project-info/memory.md`
- `/ai-rpi-protocol_project-info/user-preferences.md`

Rules:
- load both early if they exist
- keep them durable across protocol upgrades
- treat them as first-class inputs, not optional late context

### Layer 2: runtime classification

Load only what is needed to classify the work and set the initial operating posture.

Includes:
- `modes.md`
- `profiles.md`
- first-interaction behavior when relevant

Outputs:
- selected Mode
- selected Depth
- selected Persona internally
- initial load plan

### Layer 3: phase-relevant guidance


Load only the rules and phase files required for the current phase.

Examples:
- Research -> `research.md`, plus phase-triggered checks before the gate
- Plan -> `planning.md`, then planning-only rules
- Implement -> `implementation.md`, then file-change and generation rules

### Layer 4: relevant skills

Load a skill only when the user intent clearly matches it or the match is strong enough to ask.

Rule:
- skills are reusable workflows, not workers
- skills should operationalize parts of the loop proportionally
- no speculative skill loading
- once the skill match is clear, load the skill before producing substantive task output
- previously read code or prior task context is not a substitute for skill loading
- do not emit workflow-shaped output that mimics a skill without actually activating that skill

### Layer 5: relevant subagents

Use subagents when focused external context is cheaper and safer than widening the main thread.

Rule:
- widen compute before widening clutter
- prefer one focused subagent over many indiscriminate file reads
- subagents are specialist delegated workers with fresh context, not phase-bound ceremony

### Layer 6: relevant docs, artifacts, and files

Load only the files, remaining project-info, memory artifacts, templates, and repo context that the active phase actually needs.

Examples:
- specific implementation files
- project-info files tied to the task
- memory artifacts from the current task
- templates used by the current phase

### Layer 7: guardrail escalation and widening with evidence

Only widen beyond the current slice when the work proves it is necessary.

Valid triggers:
- the current evidence is insufficient to make a safe decision
- the task crossed a module or service boundary
- risk increased beyond the current Depth's safe handling range
- criticality, destructive potential, or user impact exceeded the current autonomous posture
- a hook point fired before a risky action, contract change, or critical-path modification
- a skill or subagent clearly reduces uncertainty faster than more local reading
- a prior assumption was invalidated

Invalid triggers:
- curiosity
- habit
- vague fear that more context might help
- loading a file because it is nearby

## Soft context budgets by Depth

These are soft budgets, not hard quotas. They exist to force a compaction decision before context gets sloppy.

### Minimal

Default loading shape:
- Layers 0-2
- at most one narrow Layer 5 slice

Budget guidance:
- usually 4-6 file loads total in the active loop
- avoid skills unless the task is explicitly a skill match
- prefer no subagent unless it prevents obvious rework

Compaction trigger:
- if the task starts pulling in multiple areas, stop and either escalate Depth or condense first

### Balanced

Default loading shape:
- Layers 0-2 always
- Layers 3-5 on demand

Budget guidance:
- usually 8-12 meaningful file or artifact loads in the active loop
- one focused subagent is normal when research would otherwise sprawl
- remaining project-info and session memory should be targeted, not bulk-loaded

Compaction trigger:
- if findings no longer fit in a lean summary, condense to memory or a handoff artifact before widening again

### Full

Default loading shape:
- any layer is available, but still loaded proportionally

Budget guidance:
- usually 12-20 meaningful loads before a deliberate compaction checkpoint
- multiple subagents are acceptable when the task is truly cross-cutting
- specs, memory, and review artifacts should replace repeated re-reading

Compaction trigger:
- before every major phase transition, after broad exploration, and whenever the thread starts carrying more context than the next decision needs

## Runtime transparency

Progressive loading should be visible when it materially affects behavior.

### Active signal

Use when classification or loading scope materially matters.

Format:
- `This repo has AI-RPI-Protocol available - <one short concrete benefit>. Given the request of <short request shape>, I loaded only the essentials of AI-RPI-Protocol. We're currently on Mode <Mode> and the Protocol Depth is <Depth>.`

Examples:
- `This repo has AI-RPI-Protocol available - it starts narrow so the agent doesn't overreach too early. Given the request of a quick explanation, I loaded only the essentials of AI-RPI-Protocol. We're currently on Mode Explore and the Protocol Depth is minimal.`
- `This repo has AI-RPI-Protocol available - it helps challenge weak framing before implementation drift kicks in. Given the request of helping with a colleague message, I loaded only the essentials of AI-RPI-Protocol. We're currently on Mode Discuss and the Protocol Depth is balanced.`

Rule:
- The benefit should be generated for the current situation, not picked from a fixed canned list.
- Keep it short, concrete, and user-facing.
- The request shape should be described in plain language, not internal taxonomy or file-loading jargon.
- Do not expose internal layer numbers in user-facing runtime signals.

### Explicit flagging

Use when the protocol catches a problem, blocks premature widening, or forces a reset.

Format:
- `AI-RPI flagging <what> - <why it matters>.`

Examples:
- `AI-RPI flagging missing constraints - planning would drift without them.`
- `AI-RPI flagging context drift - a clean handoff will be safer than carrying stale assumptions.`

## Phase-local compaction

Compaction is part of normal operation, not a failure state.

When to compact:
- before a phase gate when the underlying evidence is broad
- after a subagent returns a large result
- when changing topic or scope inside the same repo
- when the next decision needs conclusions, not raw search trails

Compaction options:
- write a lean research artifact to memory
- write a planning artifact instead of repeating the plan in chat
- generate a context handoff artifact for a clean restart
- summarize the active slice and drop the rest

Rule:
- phase-local summaries should preserve decisions, evidence pointers, constraints, and next steps
- they should not preserve every intermediate search path

## Progressive-loading decision tree

1. Start with Layers 0-2.
2. Does the task clearly match a skill?
   - Yes -> load Layer 3 for that skill and follow its workflow.
   - No -> continue.
3. Load the current phase file from Layer 2.
4. Can the next decision be made with the current slice?
   - Yes -> stay narrow.
   - No -> continue.
5. Would a focused subagent reduce uncertainty faster than more main-thread loading?
   - Yes -> load Layer 4.
   - No -> widen Layer 5 selectively.
6. Has risk, scope, ambiguity, or guardrail criticality increased beyond the current safe posture?
   - Yes -> escalate Depth and widen only the layers that new risk requires.
   - No -> continue with the current Depth.
7. Has the active slice become too broad for the next decision?
   - Yes -> compact before loading more.
   - No -> continue.

## Mode x Depth x loading matrix

| Mode | Minimal | Balanced | Full |
|------|---------|----------|------|
| Explore | Layers 0-2 plus one narrow evidence slice | Layers 0-2 plus targeted files or one research subagent | Layers 0-5 with broader mapping and mandatory compaction checkpoints |
| Discuss | Layers 0-2 plus only the facts needed to frame trade-offs | Layers 0-3 plus targeted architecture or product context | Layers 0-5 with broader constraint loading and richer option shaping |
| Review | Layers 0-2 plus changed files and validation evidence | Layers 0-4 plus standards or review agents as needed | Layers 0-5 plus specialist subagents and explicit packaging artifacts |
| Patch | Layers 0-2 plus the directly affected files | Layers 0-2 plus nearby tests, constraints, and one focused subagent if needed | Layers 0-5 when the patch touches sensitive areas or hidden blast radius |
| Feature | Rare; only for very small additive work | Layers 0-5 on demand with proportional shaping artifacts | Layers 0-6 with broader context, stronger planning, and repeated compaction |
| Build | Rare; only for tightly bounded execution work | Layers 0-5 with implementation-driven widening | Layers 0-6 with specs, review packaging, and cross-cutting evidence |

## Recommended modular structure

Keep progressive loading modular so the user can reason about it and teams can customize it without rewriting the whole protocol.

- `core/system/progressive-loading.md` -> product model, layers, budgets, triggers, decision tree, matrix
- `core/system/operational-units.md` -> canonical skills/subagents distinction, inventories, challenger pattern, review layers, and operational mapping
- `core/system/validation-model.md` -> canonical validation layers, confidence, uncertainty, acceptance mapping, and review triggers
- `core/system/file-index.md` -> canonical map of what can be loaded and when
- `core/rules/context-attention.md` -> operational rules for selective loading
- `core/rules/token-discipline.md` -> compaction, artifact preference, and summary rules
- `core/rules/topic-drift.md` -> when to stop carrying stale context
- `templates/project-info-generation/project-info-loading-guide.md` -> domain-specific Layer 5 loading rules
- `templates/context-handoff-artifact.md` -> clean restart packaging when compaction is not enough

This structure keeps the public concept centralized while preserving focused rules for each operational concern.
