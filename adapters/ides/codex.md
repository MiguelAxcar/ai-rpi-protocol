purpose: Codex rules and feature leverage; output: mandatory rules + features; use when: running in Codex.

# Codex IDE adapter

## Mandatory rules

### Rule 1
Anti pattern: jump into code or commands before grounding the task in the repo
Do: start with Research, read the relevant files first, and summarize findings before moving on

### Rule 2
Anti pattern: blend Research, Planning, and Implementation into one stream because the tool can do all three quickly
Do: keep phase boundaries explicit, end each entered phase with a compact synthesis, and wait at gates

### Rule 3
Anti pattern: treat discussion-only or question-only asks as outside the protocol
Do: follow the repo startup contract on every new conversation, then keep the handling proportional to the task

### Rule 4
Anti pattern: make broad edits across the workspace without keeping them reviewable
Do: keep diffs small, patch intentionally, and summarize the intent of each change batch before continuing

### Rule 5
Anti pattern: assume codebase behavior from naming or prior patterns
Do: search the workspace, cite file paths, and separate verified facts from inferences

### Rule 6
Anti pattern: act like a yes-machine when the request is vague or risky
Do: add positive friction, challenge weak framing, and present real trade-offs before implementation

### Rule 7
Anti pattern: claim success after editing without running the relevant checks
Do: run the shortest reliable validation commands for the repo, then report what ran and what remains unverified

### Rule 8
Anti pattern: let long sessions drift after new discoveries change the plan
Do: update the working summary, return to Planning when assumptions break, and keep the user aware of the reset

## Specific features

### Workspace search and file reads
When: starting Research or checking a claim
Do: search the repo, open the exact files that matter, and ground findings in concrete evidence

### Patch-oriented editing
When: in Implementation phase
Do: prefer small patch-style edits that stay easy to review and map cleanly back to the approved plan

### Shell validation
When: after any non-trivial change
Do: use shell commands to run the repo checks that matter, capture the result, and report failures clearly

### Plan tracking
When: the task spans multiple steps or the work could drift
Do: keep a short plan, update progress as work advances, and use it to preserve phase discipline

### Parallel investigation
When: Research would otherwise sprawl across several files or surfaces
Do: split narrowly scoped reads or checks, then merge the results into one concise synthesis before continuing
