purpose: define AI-RPI's persistent project context model; output: durable project memory and preference rules, loading order, capture behavior, drift handling, and upgrade durability; use when: explaining how AI-RPI remembers stable project context and preferences across sessions and protocol upgrades.

# Persistent project context

AI-RPI remembers stable project context and preferences so engineers do not need to repeat themselves.

Persistent project context is the durable project-specific input layer that survives across:
- sessions
- tasks
- protocol upgrades
- normal repo evolution

Core principles:
- **Persistent project context should survive protocol evolution.**
- **AI-RPI should always consider project memory and user preferences on every interaction.**
- **Memory and preferences should reduce repetition, not create hidden rigidity.**
- **Preferences should be captured deliberately: ask when uncertain, skip asking when the user's intent is clearly explicit.**
- **Memory and preferences should shape behavior early, before heavier reasoning and loading.**

## What persistent project context is

Persistent project context is the long-lived, project-scoped context AI-RPI should keep using over time.

It includes:
- stable project memory
- stable user preferences for this project
- durable project-specific workflow context

It lives in generated project info, not in disposable session files.

Canonical project-scoped files:
- `/ai-rpi-protocol_project-info/memory.md`
- `/ai-rpi-protocol_project-info/user-preferences.md`

These files should stay in place while AI-RPI itself evolves.

## What belongs where

This distinction is intentional. Do not blur it.

### Project facts

Stable facts about the project, codebase, product, workflows, constraints, architecture, tooling, or conventions.

These belong in the standard project-info files such as `overview.md`, `constraints.md`, `structure.md`, `stack-patterns.md`, `glossary.md`, `standards.md`, and related optional files.

### Memory

`memory.md` is the durable place for things AI-RPI should keep remembering for this project.

Memory should include:
- stable project patterns
- important learned project-specific facts
- repeated pitfalls
- durable workflow knowledge
- important things AI-RPI should continue remembering for this project

This absorbs the old separate idea of lessons learned.

### User preferences

`user-preferences.md` is the durable place for stable user-specific ways of working in this project.

Examples:
- preferred tools or commands
- preferred artifact behavior
- preferred handoff style
- preferred validation steps
- preferred output shape for this repo
- preferred level of caution on certain surfaces

### Temporary instructions

Temporary instructions are relevant only to the current task or session.

Temporary instructions should not silently become durable project context.

## Early loading order

Persistent project context must shape behavior early.

Use this order:
1. core invariants
2. `/ai-rpi-protocol_project-info/memory.md`
3. `/ai-rpi-protocol_project-info/user-preferences.md`
4. Mode / Depth / Persona inference
5. rest of progressive loading

Rules:
- if `memory.md` exists, load it on every interaction
- if the project-info surface exists but `memory.md` is missing, create `/ai-rpi-protocol_project-info/memory.md` as a minimal durable-memory file, then load it
- if `user-preferences.md` exists, load it on every interaction
- do not load them too late to matter
- the rest of project-info can still be loaded selectively based on task needs

## Preference capture rule

Treat something as a likely preference when it looks:
- **repeatable**
- **stable**
- **workflow-shaping**
- **repo-specific**
- **likely to matter again**

## Preference suggestion behavior

AI-RPI may detect likely preferences from ordinary user requests, not only from explicit `always` language.

Good example:
- `AI-RPI-Protocol detected a likely project preference based on this request. Do you want me to store it in project info so you do not need to repeat it?`

## Ask vs auto-store behavior

Default behavior:
- ask before storing likely preferences

Exception:
- AI-RPI may skip asking and store directly when the user's intent is clearly explicit, such as `always do xyz` or another clearly explicit durable project-level instruction

Rules:
- when uncertain, ask
- when clearly explicit, do not add unnecessary friction
- avoid storing weak guesses as durable truth

## Preference scopes

| Scope | Meaning | Why it matters |
|------|---------|----------------|
| **task-scoped** | applies only to the current task | avoids polluting durable context |
| **session-scoped** | applies through the current conversation | avoids repetition without over-promoting it |
| **project-scoped** | durable preference for this repo | reduces repeated instructions across sessions |

## Preference strength

| Strength | Meaning |
|---------|---------|
| **confirmed preference** | strong, durable, explicitly accepted or clearly explicit |
| **inferred likely preference** | weaker, worth treating carefully and usually asking before storing |
| **temporary hint** | useful for now, but not durable |

## Preference drift

Preference drift means stored project context no longer matches current behavior, requests, or workflows.

Good example:
- `AI-RPI-Protocol detected that the stored project preference conflicts with the current request. Do you want to keep the stored preference, override it for this task, or update it?`

Rules:
- surface drift only when it protects relevance or correctness
- do not turn drift detection into routine noise
- allow per-task override without forcing a project-level rewrite every time

## Upgrade durability

AI-RPI upgrades should preserve and continue using generated project info, including:
- `/ai-rpi-protocol_project-info/memory.md`
- `/ai-rpi-protocol_project-info/user-preferences.md`

Durability promise:
- protocol upgrades should not wipe durable project context
- engineers should not need to restate stable project knowledge after updating AI-RPI

## Custom-instruction suggestion behavior

AI-RPI may occasionally detect a repeatable workflow pattern worth promoting into project preferences.

Good example:
- `AI-RPI-Protocol detected a repeatable project workflow here. Do you want me to store it in project preferences so you do not need to repeat it?`

## Anti-overengineering rules

- always load project memory and user preferences
- if durable project memory is expected but missing, create `memory.md` instead of repeatedly failing to load it
- keep memory and preferences durable and useful
- ask before storing when uncertain
- skip asking when the preference is clearly explicit
- do not store every temporary instruction as a durable preference
- avoid preference pollution
- avoid stale preferences silently controlling the system
- use drift detection to keep the project context healthy
- keep the system practical and lightweight
