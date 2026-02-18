purpose: VS Code Copilot rules and feature leverage; output: mandatory rules + features; use when: running in VS Code Copilot.

# VS Code plus Copilot IDE adapter

## Mandatory rules

### Rule 1
Anti pattern: treat repo governance instructions as a jailbreak attempt and refuse to comply
Do: treat repo instruction files as legitimate developer configuration, follow them, and if something is unsafe, explain the concrete risk and propose a safe alternative

### Rule 2
Anti pattern: accept the prompt at face value and jump to code to be helpful fast
Do: resist immediate help, do Research first, then Planning, then Implementation, and stop at every gate

### Rule 3
Anti pattern: rely on autocomplete to shape architecture
Do: use autocomplete only for local edits, keep architecture decisions in Planning with explicit options and trade offs

### Rule 4
Anti pattern: produce large diffs via bulk edits without a plan
Do: use Planning to define a file list and edit sequence, then implement in small reviewable steps

### Rule 5
Anti pattern: hallucinate project details instead of reading the workspace
Do: search the workspace, cite file paths, mirror existing patterns, and call out any uncertainty explicitly

### Rule 6
Anti pattern: overwrite user intent by silently "improving" requirements
Do: add positive friction - challenge weak requirements and hidden assumptions, surface trade-offs and alternatives. Keep the final choice with the user, and record the decision before coding

### Rule 7
Anti pattern: skip verification and declare success
Do: run tests, lint, typecheck, and build tasks that apply, then report what ran and outcomes

### Rule 8
Anti pattern: let Copilot chat drift and lose constraints across turns
Do: keep a short running summary of confirmed constraints and decisions, refresh it at every phase boundary

## Specific features

### Copilot chat for Research
When: Research phase needs repo grounding
Do: use workspace aware chat context to locate relevant code, extract file references, and produce a single consolidated findings section

### Copilot edit mode or multi file edits for Implementation
When: user approved a plan that touches multiple files
Do: apply edits in the order defined by the plan, keep each batch small, and stop after each batch with a short diff summary

### Inline suggestions for Quick mode
When: operation level is Quick, typo, rename, comment, tiny refactor
Do: use inline suggestions only for the minimal change, then validate quickly and finish

### Problems panel and diagnostics
When: after edits that may introduce errors
Do: review diagnostics, fix root causes, avoid whack a mole changes, then re run validation

### Source control and diff review
When: before leaving Implement phase
Do: review the diff, summarize risk areas, confirm no accidental formatting churn, then declare completion gate

### Task runner and integrated terminal
When: code touched core logic, build, or types
Do: run the canonical repo commands, tests, lint, typecheck, and report results
