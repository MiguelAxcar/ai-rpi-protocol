purpose: define Implement phase contract; output: working code + continuous validation; use when: Implement phase in any mode.

# Phase: Implement

Purpose: Execute the plan with minimal disruption, validate continuously, and end with reviewable work.

---

## Internal sub-phases

Implementation contains:

- **Slice** — execute bounded units of work
- **Check** — validate quickly and often
- **Stabilize** — confirm fit with the plan, repo patterns, and surrounding constraints
- **Validate** — prove the result with layered evidence and widen into review when needed
- **Package** — produce reviewable outcomes and optionally recommend delivery artifacts

## Hook points during implementation

Implementation should respect hook points before the next risky step continues.

Common hook points:
- before risky actions
- before editing critical files or critical user flows
- before destructive commands
- before contract or interface changes
- after implementation before claiming done
- before validation summary, review package, PR description, or handoff generation

If a hook fires:
- explain briefly why it fired
- determine whether confirmation, escalation, or blocking is required
- do not silently continue past a meaningful hook on a critical surface

---

## Code generation rules

- **Minimal diffs** — change only what the plan specifies. No drive-by refactors, no style changes, no bonus improvements. If your diff touches files or lines not in the plan, justify each one.
- **Follow existing architecture** — mirror naming, error handling, folder conventions, and patterns from adjacent code. Do not introduce new patterns unless the plan explicitly justifies it.
- **Implement tasks from the plan** — follow the task order. When the plan uses a PRD or Tech Spec (see `/ai-rpi-protocol/core/phases/planning-prd-techspec-guidance.md`), parse the structured `## tasks` section: each task has `id`, `description`, `files`. Execute in order. Mark each task complete as you go. Do not reorder or skip tasks without justification.
- **Incremental changes** — implement in small, reviewable steps. Each step should be independently correct. At full Depth, each slice may be confirmed by the user before proceeding.
- **Follow durable project context** — when `/ai-rpi-protocol_project-info/memory.md` or `/ai-rpi-protocol_project-info/user-preferences.md` exist, load them and apply them to every change.

---

## Continuous validation

Do not wait until the end to verify. Validate throughout implementation.

- **Run automated tests** after each meaningful change. If tests exist, run them. If they don't, flag the gap.
- **Run build / compile** after structural changes. Catch breakage early, not at the end.
- **Generate tests** when the plan calls for them, or when critical paths lack coverage. Propose test cases and let the user decide scope.
- **Propose manual test scripts** when automated testing is insufficient or impractical. Be specific and practical: "We could test this endpoint with a curl script using dummy data — want me to generate one?" Include the actual script or commands.
- **Verify behavior changed as intended** — don't just check that code compiles. Confirm the change does what the plan said it should do. Diff before/after when relevant.
- **Map acceptance explicitly** when the task is not trivial. Compare the request, plan or spec, actual implementation, and validation evidence.
- **State uncertainty explicitly** when any important path, environment, or acceptance question remains unvalidated.
- **Escalate validation** when criticality, user impact, blast radius, or uncertainty are high. Small diff does not mean low validation needs.
- **Escalate guardrails** when destructive potential, critical surfaces, weak evidence, or unresolved uncertainty mean autonomy should tighten before proceeding.

---

## Validation and review assistance

After implementation, help the engineer understand the validation status and review the result.

- Summarize what changed and where (files, functions, lines)
- Explain why the change exists and what problem it solves
- State which trade-offs were chosen
- Highlight anything that deviated from the plan (with justification for each deviation)
- Show the strongest validation evidence and the weakest evidence
- Point out areas that need manual review or testing
- State confidence as low / medium / high when it materially affects trust in the result
- Surface remaining uncertainty and what would reduce it
- Provide reviewer focus so the next reader knows where scrutiny matters most
- Propose additional validation if appropriate
- If tests were generated, summarize coverage and any gaps
- If manual test scripts were proposed, include them ready to run
- Recommend useful delivery artifacts when they help: PR description, handoff note, review package, validation summary, diagram, QA checklist, or another packaging artifact
- If a heavier delivery artifact would help, explain why and ask before generating it unless the user already asked for it.
- Surface artifact drift when the request, shaping artifact, implementation, validation evidence, and delivery artifact no longer line up.
- Before packaging reviewer-facing outputs, use a hook to ensure the summary does not hide guardrail triggers, weak evidence, or criticality.

---

## Invariant rules

- Implementation must follow the plan. If you need to deviate, stop and ask before deviating.
- No scope expansion. If you see something else to fix, note it for later — do not fix it now.
- No untested critical paths. If you can't test something, say so and explain why.
- Minimal diffs are not optional. Every changed line must trace back to a planned task.
- Run tests continuously, not just at the end. If a test breaks mid-implementation, stop and address it before continuing.
- Validation claims must be evidence-backed. Do not say "done" without making uncertainty and evidence visible.
- If the plan breaks (core assumption was wrong, approach is unworkable), stop. Explain what broke and why. Return to Plan with new information. This is not a failure — plans are hypotheses; implementation is the test.

---

## Checklist

Before declaring implementation complete, verify:

- [ ] All planned tasks implemented
- [ ] Automated tests run and passing (or flagged if unavailable)
- [ ] Build / compile succeeds (or flagged if not applicable)
- [ ] New tests generated where appropriate
- [ ] Manual test scripts proposed where appropriate
- [ ] Behavior verified — change does what the plan intended
- [ ] Acceptance mapping checked
- [ ] Remaining uncertainty stated
- [ ] Confidence calibrated where it matters
- [ ] Diff is minimal — no unplanned changes
- [ ] No architectural drift from existing patterns
- [ ] Summary of changes prepared for engineer review
- [ ] Reviewable packaging prepared
- [ ] Delivery artifact recommendations justified before generation
- [ ] Deviations from plan documented with justification

---

## Memory (before completion)

Write to memory if the protocol level requires it:
- `/ai-rpi-protocol/memory/session-state.md` — updated status
- `/ai-rpi-protocol/memory/decisions.md` — only if new decisions occurred during implementation
- `/ai-rpi-protocol/memory/metrics-log.md` — append one lean row when useful for outcome and protocol-quality trends:
  - Date, task name, mode, depth
  - Outcome quality and noise level
  - Meaningful corrections or structural overrides
  - Validation strength
  - Whether AI-RPI should have flexed more or held firmer
  - Notes: one-line summary of what helped or hurt

- `/ai-rpi-protocol_project-info/memory.md` — append a concise durable lesson when user correction or failure reveals a repeatable project pattern

If `/ai-rpi-protocol_project-info/memory.md` is missing but durable project context is otherwise in use, create it before writing the lesson.

Memory is silent — update before presenting the completion summary.

---

## On files changed

Whenever project files are created, modified, or deleted:
- Run lint (and typecheck/tests if applicable)
- Check if project-info needs updating
- Run the code-generation-rules checklist from `/ai-rpi-protocol/core/rules/code-generation-rules.md`

See `/ai-rpi-protocol/core/rules/on-files-changed.md` for details.

---

## Delegation guidance

Implementation can stay in the main thread or use focused subagents when diagnosis, specialist review, or reviewer packaging would materially improve the outcome.

Typical Implementation subagents:
- `debugger` when the root cause is still not settled
- `code-reviewer` when a fresh review lens is cheaper than later rework
- `security-reviewer` or `performance-reviewer` when the change crosses those risk surfaces
- `standards-discovery` when implementation style conventions are still unclear
- `conventions-reviewer`, `patterns-reviewer`, `test-quality-reviewer`, or `documentation-reviewer` when those review lenses materially affect release confidence
- `packaging-reviewer` when the result needs a stronger review package or handoff

If delegating:
- pass the approved plan, relevant code context, and this phase file
- keep the delegated job narrow and outcome-oriented
- keep the main agent responsible for synthesis, scope control, and user-facing output

---

## Challenge and friction

Even during implementation, the protocol pushes back.

- If the plan's approach turns out to be harder than expected, flag it. Don't silently work around it.
- If you see a risk the plan missed, surface it before continuing.
- If the existing code has patterns that conflict with the plan, flag the conflict. Don't silently override either side.
- If test coverage is insufficient for the change, say so explicitly and propose what to add.
- If a "quick fix" temptation arises (skip tests, hardcode a value, ignore an edge case), resist it and flag it.
- If a risky or critical action needs explicit confirmation, stop and ask instead of silently pushing through.

Format: `"AI-RPI flagging <what> - <why it matters>."`

---

## Output format

```
Changes:
- <file>: <what changed>

Why:
- <problem solved>

Trade-offs:
- <chosen trade-off>

Validation:
- Checks: <tests/build/lint/scripts>
- Behavior: <what was checked and result>
- Acceptance mapping: <matched / partial / unmet, with brief evidence>
- Confidence: <low / medium / high> — <why>
- Remaining uncertainty: <what is still unverified>
- Proposed manual tests: <scripts or commands, if any>

Reviewer focus:
- <what reviewers should inspect>

Deviations from plan: <none, or list with justification>
Optional next outputs: <PR description | handoff note | review package | validation summary | diagram | QA checklist | none>
```

---

## Completion

"Implementation complete. [summary of what changed]. If useful, I can also prepare a PR description, handoff note, review package, validation summary, diagram, QA checklist, or another next-step artifact."
