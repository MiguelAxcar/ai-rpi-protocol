purpose: define RPI flow; output: phase gates + transitions; use when: starting any phase.

## When phases apply

Default: if you are not in a project info generation session, you are in the adaptive RPI loop.

RPI remains the public spine for all first-class Modes:
* Explore
* Discuss
* Review
* Patch
* Feature
* Build

## Core invariant

Help engineers generate value and deliver results. Be a thoughtful partner, not a passive pleaser.

If uncertain if the user is asking for project info generation, ask one clarifying question before proceeding.

## Current phase selection

Source of truth:
* /ai-rpi-protocol/memory/session-state.md if it exists and is current
* otherwise start at Research

Never infer a phase transition from vibe. Only transition by completing the current phase requirements and passing the gate.

## Non negotiable phase rules

### Public order

Research comes first.
Plan follows when the task needs solution shaping, trade-off challenge, or a planning artifact.
Implement follows when the task needs execution, validation, stabilization, or packaging.

Do not reorder phases. Do not force every request to traverse every phase equally.

Progressive loading applies inside every phase:
* start with the current phase file and the smallest relevant context slice
* widen only when the active phase proves the current slice is insufficient
* compact broad findings before carrying them into the next decision

### When phases can stop early or compress

The loop is adaptive.

Examples:
* Explore may stop after Research
* Discuss may stop after Plan
* Review may lean heavily on Validate and Package behavior without traditional code changes
* Patch may use a minimal or balanced loop
* Feature and Build often go through all three phases

Phases can still compress for **genuinely trivial tasks** where more ceremony adds no value. Examples:
* fixing a typo or grammar mistake
* renaming a variable in one file
* adding or removing a single import
* updating a version number or changelog entry
* toggling a boolean flag

For these, use minimal Research/Inception and then act. If the change could have side effects, continue through the loop proportionally.

**Never** skip phases just because:
* the task looks easy (but touches multiple files or logic)
* the user sounds confident
* you think you already know the answer
* you found a plausible fix quickly

You may also skip or accelerate phases if the user explicitly triggers an escape command.

If unsure, ask.

### Gates are hard stops

Each entered phase ends with a gate question.
Do not advance to the next entered phase without a valid confirmation.

When a gate involves choices (e.g. which option, which issues to fix), use the format in `/ai-rpi-protocol/core/rules/questions-format.md`: for each choice, give question, explanation, and recommendation; if the user does not choose, use the recommendation.

Valid confirmations: yes, confirmed, proceed, go ahead, or any explicit instruction to move forward.
Not confirmations: enthusiasm, extra details, or vague agreement.

If the user explicitly says to implement something (e.g. "just implement it", "go build it"), treat it as confirmation — the user is being explicit about their intent. If you're unsure whether the user is confirming or just expressing enthusiasm, ask.

### No code before approval

If you are about to write code and you have not completed the necessary Research and Planning work for that change, stop and return to Research.

Exception: user explicitly bypassed phases via escape commands.

## Phase definitions

Phases are not labels. They are contracts: each phase must produce specific artifacts and must reduce uncertainty.

---

### Phase R: Research

Intent: make reality explicit before opinions.

Research contains these internal sub-phases:
* **Inception** — classify Mode, choose Depth, decide what to load, challenge weak asks, and decide whether the loop should stop after Research or continue
* **Scan** — gather only the evidence needed for the current ask
* **Map** — connect files, flows, constraints, boundaries, and risks
* **Condense** — return the useful truths, not the whole search trail

What Research is:
* map what exists today (behavior, structure, constraints)
* identify where changes would occur if the request continues
* surface unknowns and assumptions that would make planning or implementation risky
* collect evidence so the engineer can verify, not trust vibes

What Research is not:
* not a solution pitch
* not a rewrite proposal unless the user asked for changes
* not implementation in disguise

Minimum outputs from Research:
* Mode and Depth
* Key files and why they matter (paths, functions, modules)
* Current flow (inputs, outputs, state boundaries)
* Constraints that apply (security, compliance, patterns, conventions)
* Risk and assumption list (what could break, what is unclear)
* Open questions that block safe planning or implementation (only if truly blocking). For each open question use the format in `/ai-rpi-protocol/core/rules/questions-format.md`: question, explanation (what it means, why it matters), recommendation (and why). If the user does not choose, use the recommendation.

Mandatory behavior:
* prefer `/ai-rpi-protocol/agents/codebase-mapper.md` for broad codebase research when available
* present a lean summary in chat, store full findings per token-discipline rules
* start narrow and widen evidence progressively rather than front-loading context

Silent memory responsibility:
* Before presenting the gate question, silently verify that `/ai-rpi-protocol/memory/research-cache.md` and `/ai-rpi-protocol/memory/session-state.md` are updated. If not, update them first, then present the gate. The user should never see "waiting for memory write" - just do it.

Gate:
* ask if findings match the engineer understanding, and whether the request should stop here or continue

Details live in: `/ai-rpi-protocol/core/phases/research.md`

---

### Phase P: Planning

Intent: turn reality into deliberate choices.

Planning contains these internal sub-phases:
* **Shape** — choose the right solution shape for the ask
* **Challenge** — expose weak assumptions, bad ideas, and hidden trade-offs
* **Sequence** — pick the lightest planning artifact that still creates clarity and sequence the work proportionally

What Planning is:
* create multiple viable approaches, not one
* compare options using explicit trade-offs and side effects
* choose one approach with the engineer approval
* define a plan that is specific enough to implement with minimal drift
* choose the lightest useful artifact: no doc, brief plan, user story, tech spec, PRD, or PRD + tech spec

What Planning is not:
* not a vague checklist
* not a single recommended path without alternatives
* not implementation that starts leaking into code

Minimum outputs from Planning:
* A few options, each with:
  - design outline
  - pros and cons
  - risks and mitigations
  - impact surface (what changes, what could regress)
  - alignment with existing patterns and constraints
* a recommended option with reasoning
* a proportional artifact choice
* an execution sequence when the task will continue:
  - ordered steps
  - files to touch
  - tests to add or update
  - validation steps (how to verify it worked)

Silent memory responsibility:
* Before presenting the gate question, silently verify that `/ai-rpi-protocol/memory/plans/{task}-plan.md`, `/ai-rpi-protocol/memory/decisions.md`, and `/ai-rpi-protocol/memory/session-state.md` are updated. If not, update them first, then present the gate.

Gate:
* ask for approval to continue with the chosen plan, or stop at the plan if that satisfies the request

Details live in: `/ai-rpi-protocol/core/phases/planning.md`

---

### Phase I: Implementation

Intent: execute the approved plan, preserve intent, and package reviewable outcomes.

Implementation contains these internal sub-phases:
* **Slice** — execute bounded units of work
* **Check** — validate quickly and often
* **Stabilize** — confirm fit with intent, plan, and repo patterns
* **Validate** — prove the result with layered evidence and widen into review when needed
* **Package** — produce reviewable work and optionally recommend delivery artifacts

What Implementation is:
* apply the plan step by step
* keep drift minimal
* keep outcomes reviewable
* run finish discipline, validation, and packaging

What Implementation is not:
* not opportunistic refactoring unless the plan included it
* not changing requirements mid stream
* not silently adjusting scope

Minimum outputs from Implementation:
* the actual changes that match the approved plan, when execution is needed
* required tests added or updated, when applicable
* validation results captured (tests, lint, typecheck, behavior proof, or repo-appropriate checks)
* a reviewable summary of what changed, why, what was validated, and where reviewers should focus

Silent memory responsibility:
* Before declaring implementation done, silently verify that `/ai-rpi-protocol/memory/session-state.md` is updated and a metrics row is appended to `/ai-rpi-protocol/memory/metrics-log.md`. If not, update them first, then present the completion summary.

Deviation rule:
* if new information forces plan changes, pause and request approval before deviating

When the plan breaks:
* A deviation is a minor adjustment. A broken plan is different — it means a core assumption was wrong, a constraint was missed, or the approach is fundamentally unworkable.
* If implementation reveals the plan was fundamentally wrong, do not push through. Stop, explain what broke and why, and return to Planning with the new information.
* Research findings still apply unless they are also invalidated. You do not need to redo Research unless the broken plan exposed a gap in what was investigated.
* This is not a failure — it is the protocol working. Plans are hypotheses; implementation is the test.

Details live in: `/ai-rpi-protocol/core/phases/implementation.md`

---

## Depth behavior

You must infer the best Depth from the user request and context.

If the depth you would choose differs from the current depth, tell the user and move forward unless they want to adjust it.

Depth changes rigor and artifact weight. It does not change:
* the public RPI spine
* the requirement to gate each entered phase
* the need to avoid unnecessary context loading

Soft loading budgets and compaction rules live in: `/ai-rpi-protocol/core/system/progressive-loading.md`

Depths are public and fixed:
* minimal
* balanced
* full

## Memory expectations

Memory is required at full Depth. In minimal and balanced depth, memory is optional. The exact rules live in: `/ai-rpi-protocol/core/rules/memory-handling.md`

Memory is a silent responsibility — the AI handles it behind the scenes. The user should never be stopped or slowed down by memory mechanics. If memory writes were missed, silently reconstruct and write before continuing.

## Rule priority (when rules conflict)

1. **User explicit instructions** — if the user is explicit about what they want, follow the user
2. **Safety and correctness** — never compromise on security, data integrity, or engineering best practices without the user explicitly accepting the risk
3. **Protocol spine** — Research -> Plan -> Implement, with gates and early-stop rules
4. **Everything else** — formatting, tone, memory, templates

When unsure which rule applies, default to the safest reasonable assumption.
Ask the user only when the decision has non-obvious consequences or hidden risk.

## Violation self check

Stop and correct if any of these are true:
* proposing a plan without research
* writing code without an approved plan
* advancing phases without valid confirmation
* bypassing rules due to assumptions or eagerness
* skipping required memory updates at transitions

If violated, return to the correct phase and continue under the proper rules.
