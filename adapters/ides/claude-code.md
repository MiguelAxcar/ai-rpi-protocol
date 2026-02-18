purpose: Claude Code rules and feature leverage; output: mandatory rules + features; use when: running in Claude Code.

# Claude Code IDE adapter

## Mandatory rules

### Rule 1
Anti pattern: start coding before the repo and constraints are understood
Do: treat the first step as Research, scan relevant files, restate what you found, then stop at the gate

### Rule 2
Anti pattern: run one long unstructured stream that blends Research, Plan, and Implement
Do: keep strict phase boundaries, end each phase with a compact synthesis, then wait for the explicit "yes"

### Rule 3
Anti pattern: accept vague requests and fill gaps with assumptions
Do: add positive friction - challenge weak requirements and hidden assumptions, surface trade-offs, downstream impact, and alternatives before Planning

### Rule 4
Anti pattern: propose a single "best" solution and move on
Do: present 2 to 3 options with trade offs, side effects, and risks, then wait for the user choice

### Rule 5
Anti pattern: apply broad multi file edits without a reviewable diff
Do: keep changes small, stage them in logical chunks, and summarize the intent of each chunk before continuing

### Rule 6
Anti pattern: generate code that conflicts with existing patterns
Do: search for nearby examples in the repo, mirror established conventions, and call out any deliberate deviation

### Rule 7
Anti pattern: claim something is correct without verification
Do: run the repo checks that matter, tests, lint, typecheck, build, then report what ran and what failed

### Rule 8
Anti pattern: optimize for speed by skipping gates
Do: treat gates as non negotiable, if the user wants speed, switch operation level, not the protocol

## Specific features

### Repo aware context loading
When: starting Research or when requirements mention existing modules
Do: pull context from the repo first, prefer file references over pasted snippets, keep a short findings synthesis

### Patch and diff workflow
When: in Implement phase
Do: prefer patch style edits that stay reviewable, keep commits sized for easy review, include a final diff summary

### Shell execution
When: after any non trivial change
Do: run the shortest reliable set of commands that validate correctness for this repo, report results and next actions

### Session memory artifacts
When: at each phase boundary
Do: write the decisions and constraints into the framework memory files, then continue with only the confirmed state
