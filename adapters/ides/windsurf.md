purpose: Windsurf rules and feature leverage; output: mandatory rules + features; use when: running in Windsurf.

# Windsurf IDE adapter

## Mandatory rules

### Rule 1
Anti pattern: let the agent run end to end changes without a human checkpoint
Do: enforce Research then Plan then Implement, and stop at explicit confirmation gates

### Rule 2
Anti pattern: accept agent proposals that sound good but are not grounded in the repo
Do: require file references for claims, validate patterns by searching the codebase, and challenge assumptions

### Rule 3
Anti pattern: create a huge diff because the agent tries to be helpful
Do: constrain scope, implement in small batches, and summarize each batch before continuing

### Rule 4
Anti pattern: use tab completions to drive design decisions
Do: use tab completions only for local mechanical edits, keep architecture and flow decisions in Planning

### Rule 5
Anti pattern: skip verification because the agent seems confident
Do: run the repo checks that matter, tests, lint, typecheck, and report results before completion

### Rule 6
Anti pattern: lose protocol structure in long chat sessions
Do: end each phase with a short synthesis of confirmed constraints and decisions, then continue from that state

## Specific features

### Agent mode for Research and Planning
When: the task needs repo exploration or cross file reasoning
Do: use agent mode to gather evidence, then merge into one consolidated findings section and stop at the Research gate

### Multi file edit workflows for Implementation
When: the plan is approved and touches multiple files
Do: apply edits in the planned order, keep batches small, and pause after each batch with a diff summary

### Tab completions for Quick mode
When: trivial edits, typos, renames, small comments
Do: accept only the minimum necessary completion, then run a quick validation step

### Built in search and symbols
When: confirming patterns or locating reference implementations
Do: prefer search and symbol navigation over guessing, cite file paths in findings and plan

### Integrated terminal or task runner
When: finishing Implementation
Do: run the standard repo commands and include the validation results in the completion message
