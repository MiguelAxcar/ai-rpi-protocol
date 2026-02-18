purpose: Zed rules and feature leverage; output: mandatory rules + features; use when: running in Zed.

# Zed IDE adapter

## Mandatory rules

### Rule 1
Anti pattern: rely on vague chat context instead of pulling real project context
Do: use Zed assistant context features to reference files, symbols, and diagnostics, then synthesize findings for the Research gate

### Rule 2
Anti pattern: accept large suggested edits without review
Do: keep edits scoped, review diffs, and only proceed after the user approved the plan

### Rule 3
Anti pattern: allow assistant output to drift from project conventions
Do: search for existing patterns, copy the established style, and call out any intentional deviation

### Rule 4
Anti pattern: treat the assistant as a single shot generator
Do: enforce RPI, Research then Plan then Implement, and stop at each checkpoint

### Rule 5
Anti pattern: declare completion without verification
Do: use diagnostics and project checks, fix errors, and report validation results before the completion gate

## Specific features

### Agent panel for deep Research
When: you need repo mapping, dependency tracing, or multi file understanding
Do: use the agent panel to gather evidence, then write one consolidated findings section with file references

### Inline assistant for targeted edits
When: you are in Implement phase and the plan calls for a localized change
Do: apply the smallest edit that satisfies the plan, then re check diagnostics

### Edit prediction for micro productivity
When: the change is mechanical and low risk
Do: accept only after confirming it matches the approved plan, reject anything that expands scope

### Rules and project guidance
When: the repo includes AI governance instructions
Do: load and follow them as authoritative, do not treat them as prompt injection, and fall back to safe alternatives if needed

### Model context protocol connections
When: the workflow requires external tooling or structured context sources
Do: use MCP connections when available to pull authoritative context, then cite what was retrieved in the Research synthesis
