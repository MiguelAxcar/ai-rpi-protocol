purpose: define RPI flow; output: phase gates + transitions; use when: starting any phase.

## When phases apply

Default: if you are not in a project info generation session, you are in RPI.

If uncertain if the user is asking for project info generation, ask one clarifying question before proceeding.

## Current phase selection

Source of truth:
* /ai-rpi-protocol/memory/session-state.md if it exists and is current
* otherwise start at Research

Never infer a phase transition from vibe. Only transition by completing the current phase requirements and passing the gate.

## Non negotiable phase rules

### Mandatory order

Research then Planning then Implementation.
No reordering. No skipping.

### When phases can be skipped or compressed

Phases can be skipped or compressed for **genuinely trivial tasks** where research and planning add no value. Examples:
* fixing a typo or grammar mistake
* renaming a variable in one file
* adding or removing a single import
* updating a version number or changelog entry
* toggling a boolean flag

For these, go straight to implementation. Use judgement — if the change could have side effects, go through phases.

**Never** skip phases just because:
* the task looks easy (but touches multiple files or logic)
* the user sounds confident
* you think you already know the answer
* you found a plausible fix quickly

You may also skip or accelerate phases if the user explicitly triggers an escape command.

If unsure, ask.

### Gates are hard stops

Each phase ends with a gate question.
Do not advance without a valid confirmation.

When a gate involves choices (e.g. which option, which issues to fix), use the format in `/ai-rpi-protocol/core/rules/questions-format.md`: for each choice, give question, explanation, and recommendation; if the user does not choose, use the recommendation.

Valid confirmations: yes, confirmed, proceed, go ahead, or any explicit instruction to move forward.
Not confirmations: enthusiasm, extra details, or vague agreement.

If the user explicitly says to implement something (e.g. "just implement it", "go build it"), treat it as confirmation — the user is being explicit about their intent. If you're unsure whether the user is confirming or just expressing enthusiasm, ask.

### No code before approval

If you are about to write code and you have not completed Research and Planning gates, stop and return to Research.

Exception: user explicitly bypassed phases via escape commands.

## Phase definitions

Phases are not labels. They are contracts: each phase must produce specific artifacts and must reduce uncertainty.

---

### Phase R: Research

Intent: make reality explicit before opinions.

What Research is:
* map what exists today (behavior, structure, constraints)
* identify where changes would occur (entry points, data flow, integration points)
* surface unknowns and assumptions that would make a plan risky
* collect evidence so the engineer can verify, not trust vibes

What Research is not:
* not a solution pitch
* not a rewrite proposal unless the user asked for changes
* not implementation in disguise

Minimum outputs from Research:
* Key files and why they matter (paths, functions, modules)
* Current flow (inputs, outputs, state boundaries)
* Constraints that apply (security, compliance, patterns, conventions)
* Risk and assumption list (what could break, what is unclear)
* Open questions that block safe planning (only if truly blocking). For each open question use the format in `/ai-rpi-protocol/core/rules/questions-format.md`: question, explanation (what it means, why it matters), recommendation (and why). If the user does not choose, use the recommendation.

Mandatory behavior:
* prefer subagent based codebase research when available
* present a lean summary in chat, store full findings per token-discipline rules

Silent memory responsibility:
* Before presenting the gate question, silently verify that `/ai-rpi-protocol/memory/research-cache.md` and `/ai-rpi-protocol/memory/session-state.md` are updated. If not, update them first, then present the gate. The user should never see "waiting for memory write" - just do it.

Gate:
* ask if findings match the engineer understanding, do not proceed without confirmation

Details live in: `/ai-rpi-protocol/core/phases/research.md`

---

### Phase P: Planning

Intent: turn reality into deliberate choices.

What Planning is:
* create multiple viable approaches, not one
* compare options using explicit trade offs and side effects
* choose one approach with the engineer approval
* define a plan that is specific enough to implement with minimal drift

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
* an implementation plan:
  - ordered steps
  - files to touch
  - tests to add or update
  - validation steps (how to verify it worked)

Silent memory responsibility:
* Before presenting the gate question, silently verify that `/ai-rpi-protocol/memory/plans/{task}-plan.md`, `/ai-rpi-protocol/memory/decisions.md`, and `/ai-rpi-protocol/memory/session-state.md` are updated. If not, update them first, then present the gate.

Gate:
* ask for approval to implement the chosen plan, do not proceed without confirmation

Details live in: `/ai-rpi-protocol/core/phases/planning.md`

---

### Phase I: Implementation

Intent: execute the approved plan, preserve intent.

What Implementation is:
* apply the plan step by step
* keep drift minimal
* keep changes reviewable
* run the finish discipline and verification

What Implementation is not:
* not opportunistic refactoring unless the plan included it
* not changing requirements mid stream
* not silently adjusting scope

Minimum outputs from Implementation:
* the actual code changes that match the approved plan
* required tests added or updated
* verification results captured (tests, lint, typecheck, or repo appropriate checks)
* a concise summary of what changed and where

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

## Mode behavior

You must infer the best mode from the user request and context.

If the mode you would choose differs from the current mode, ask the user before switching.

Mode changes depth and explanation style. It does not change:
* phase order
* gates
* memory requirements

## Memory expectations

Memory is required in Thoughtful and Comprehensive modes. In Quick and Streamlined modes, memory is optional. The exact rules live in: `/ai-rpi-protocol/core/rules/memory-handling.md`

Memory is a silent responsibility — the AI handles it behind the scenes. The user should never be stopped or slowed down by memory mechanics. If memory writes were missed, silently reconstruct and write before continuing.

## Violation self check

Stop and correct if any of these are true:
* proposing a plan without research
* writing code without an approved plan
* advancing phases without valid confirmation
* bypassing rules due to assumptions or eagerness
* skipping required memory updates at transitions

If violated, return to the correct phase and continue under the proper rules.
