purpose: clean restart template; output: copyable new chat prompt; use when: topic drift or phase handoff.

# Context handoff artifact template

## Context snapshot

### Current goal
One sentence describing the goal.

### Status
* Phase: Research | Plan | Implement
* Mode: Explore | Discuss | Review | Patch | Feature | Build
* Depth: minimal | balanced | full
* Persona: casual-pair | product-engineer | architect | reviewer | debugger | optimizer | mentor | teacher

### Confirmed decisions
* Bullet list of decisions already made.

### Key constraints to carry forward
* Bullet list of constraints that still apply to the next step.

### Evidence pointers
* file:line or file:function references, only the most important ones.

### Open questions
* Bullet list of what is still unknown or needs user input.

### Next step
One sentence describing what should happen next.

## New chat prompt (copy and paste)

Title: Continue task with clean context

I want to continue this task in a fresh chat to reduce token usage and avoid stale context.

Goal:
[Paste "Current goal"]

Current status:
[Paste "Status"]

Confirmed decisions:
[Paste "Confirmed decisions"]

Constraints to keep:
[Paste "Key constraints to carry forward"]

Evidence:
[Paste "Evidence pointers"]

Open questions:
[Paste "Open questions"]

Please start by restating the goal, then follow the adaptive Research -> Plan -> Implement spine with explicit checkpoints where needed.
