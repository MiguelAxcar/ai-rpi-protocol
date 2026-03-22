purpose: define Research phase contract; output: problem clarity + codebase evidence; use when: Research phase in any level that executes phases.

# Phase: Research

Purpose: Understand the request, classify it correctly, and gather the right amount of evidence before proposing solutions.

Help engineers generate value and deliver results. Be a thoughtful partner, not a passive pleaser.

---

## Internal sub-phases

Research is the public first phase and also the internal controller.

### Inception

Before loading broad context, clarify what you are solving.

Produce:

- **Mode** — Explore, Discuss, Review, Patch, Feature, or Build
- **Depth** — minimal, balanced, or full
- **Persona** — selected internally to guide emphasis, browsing, and output defaults; do not surface by default
- **Problem statement** — what is broken, missing, or needed. One paragraph max.
- **Inferred user story** — when useful: "As a [who], I want [what], so that [why]." Infer from context and confirm when it matters.
- **Desired outcome / success criteria** — what does "done" look like? Be specific and measurable.
- **Acceptance anchors** — what later validation must prove true if the work continues?
- **Assumptions** — what are you assuming that has not been stated?
- **Unknowns** — what information is missing that could change the path?
- **Loop decision** — can the request stop after Research, or should it continue to Plan or Implement?
- **Initial load plan** — which layers or targeted files are enough to start safely?

Internal guidance:
- Use the change-magnitude heuristic (`tiny`, `bounded`, `meaningful`, `systemic`) to support classification.
- When unsure between two classifications, choose the simpler one first and escalate only with evidence.
- Do not mirror the user's urgency or confidence.
- Start with the minimum useful context slice and widen only when the evidence requires it.

Present the important parts to the user before going wider. Surface Mode and Depth when they materially matter. Keep Persona mostly internal.

### Scan

Load only the smallest relevant context slice.

Produce:

- **Relevant modules** — files, functions, classes that are involved or affected. Include paths.
- **Immediate signals** — the fastest evidence that confirms or challenges the user framing.
- **Escalation trigger** — what would justify widening the search?

### Map

Connect the evidence into something usable.

Produce:

- **Architecture patterns** — how is the area structured? What conventions does it follow?
- **Data flow** — how does data move through the relevant paths?
- **Constraints** — security, performance, compliance, existing contracts, backward compatibility.
- **Historical context** — why does the code look the way it does? Check git blame, comments, related decisions when useful.

### Condense

Turn the findings into a reviewable summary.

Produce:

- **What is true now**
- **What remains uncertain**
- **Why the request should stop or continue**
- **What to carry forward** — the minimum evidence and constraints the next phase needs

---

## Invariant rules

These are hard stops. Violating any of these is a protocol failure.

- No code changes during Research. Not even "small fixes."
- No solution pitching. Research is about what IS, not what SHOULD BE. Do not leak plans, options, or implementation ideas.
- No skipping Inception. Classification before broad exploration.
- Challenge assumptions. If the user's framing seems off, say so with evidence.
- Expose trade-offs even at discovery stage. If you find something the user should know, surface it.
- Prefer evidence (file paths, function names, line numbers) over narrative. If you can't prove it, say so.

---

## Checklist

Before presenting findings, verify:

- [ ] Mode identified
- [ ] Depth selected
- [ ] Problem statement is clear and confirmed
- [ ] User story inferred and confirmed when useful
- [ ] Success criteria defined
- [ ] Acceptance anchors identified when the task may continue into execution
- [ ] Assumptions listed and acknowledged
- [ ] Unknowns highlighted
- [ ] Relevant modules identified with file paths
- [ ] Architecture patterns described
- [ ] Data flow traced
- [ ] Constraints identified
- [ ] Historical context gathered (where available)

---

## Output format

Present findings as structured bullets. Keep it lean — evidence over narrative.

```
Mode: <Explore | Discuss | Review | Patch | Feature | Build>
Depth: <minimal | balanced | full>
Problem: <one paragraph>
User story: As a <who>, I want <what>, so that <why>. <optional>
Success criteria: <what done looks like>
Acceptance anchors: <what later validation must prove>
Initial load plan: <starting layers or targeted files>

Findings:
- Relevant modules: <paths>
- Architecture: <patterns>
- Data flow: <how data moves>
- Constraints: <what limits the solution>
- Historical context: <why it is the way it is>
- Escalation trigger: <what would justify widening>

Assumptions: <list>
Unknowns: <list>
Risks: <what could go wrong>
Next decision: <stop after Research | continue to Plan | continue to Implement>
```

---

## Memory (before the gate)

Write to memory if the protocol level requires it:
- `/ai-rpi-protocol/memory/research-cache.md` — full findings with evidence
- `/ai-rpi-protocol/memory/session-state.md` — current phase and task status
- `/ai-rpi-protocol/memory/decisions.md` — only if a decision was forced during research

Memory is silent — the user should never see "waiting for memory write." Update before presenting the gate.

---

## Delegation guidance

Research can stay in the main thread or use a focused subagent when fresh context, isolation, or specialist perspective would materially improve the outcome.

Typical Research subagents:
- `codebase-mapper` when repo mapping is still incomplete
- `documentation-researcher` when external references matter
- `web-researcher` when recency-sensitive external facts matter
- `standards-discovery` when local conventions influence the decision
- `debugger` when diagnosis is the real job
- `challenger` when the framing itself needs pressure

If delegating:
- pass the confirmed framing, Mode, Depth, and this phase file
- ask for structured findings with evidence
- keep the job narrow and decision-oriented

Delegation should sharpen Research, not turn it into ceremony.

---

## Challenge and friction

Research is the first place where the protocol pushes back.

- If the user's problem statement is vague, ask for clarity. Do not guess and build on guesses.
- If the user's assumptions seem wrong, challenge them with evidence from the codebase.
- If you find constraints the user did not mention, surface them prominently.
- If the desired outcome is unrealistic given what you found, say so.
- If the scope is larger than the user implied, flag it.
- Avoid loading unnecessary context for trivial work.
- If the request is really diagnosis work, keep it under Explore. Diagnose is not a public top-level kind.

Format: `"AI-RPI flagging <what> - <why it matters>."`

---

## Gate

"Does this match your understanding? Should we stop here, shape a plan, or continue into execution?"

Do not proceed without explicit confirmation.
