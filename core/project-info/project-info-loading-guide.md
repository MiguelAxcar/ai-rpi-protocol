purpose: load project truths; output: what to load based on task; use when: before Research if project-info exists.

# Project-Info Loading Guide

## When to Load Which Files

Project-info files should be loaded **on demand** based on the current phase and task requirements.

---

### Phase R: Research

**Always Load (if exists):**
- `/ai-rpi-protocol_project-info/overview.md` - Understand what the project is, domain, tech stack
- `/ai-rpi-protocol_project-info/constraints.md` - Understand limitations and rules before researching
- `/ai-rpi-protocol_project-info/custom-instructions.md` - User preferences and custom instructions (honor in all phases)

**Load When Relevant:**
- `/ai-rpi-protocol_project-info/structure.md` - When navigating codebase to find relevant files
- `/ai-rpi-protocol_project-info/glossary.md` - When encountering domain terms you need to understand
- `/ai-rpi-protocol_project-info/integrations.md` - When research involves external APIs or services
- `/ai-rpi-protocol_project-info/monitoring.md` - When researching logging, metrics (optional file)

### Phase P: Planning

**Always Load (if exists):**
- `/ai-rpi-protocol_project-info/constraints.md` - Ensure plans respect non-negotiable rules
- `/ai-rpi-protocol_project-info/stack-patterns.md` - Follow established patterns in plan
- `/ai-rpi-protocol_project-info/custom-instructions.md` - User preferences and custom instructions

**Load When Relevant:**
- `/ai-rpi-protocol_project-info/standards.md` - When planning code structure or testing approach
- `/ai-rpi-protocol_project-info/structure.md` - When planning new modules or architectural changes
- `/ai-rpi-protocol_project-info/integrations.md` - When planning integration with external services
- `/ai-rpi-protocol_project-info/monitoring.md` - When planning observability (optional file)

### Phase I: Implementation

**Always Load (if exists):**
- `/ai-rpi-protocol_project-info/constraints.md` - Enforce rules during implementation
- `/ai-rpi-protocol_project-info/stack-patterns.md` - Follow patterns consistently
- `/ai-rpi-protocol_project-info/standards.md` - Apply code style and conventions
- `/ai-rpi-protocol_project-info/custom-instructions.md` - User preferences and custom instructions

**Load When Relevant:**
- `/ai-rpi-protocol_project-info/structure.md` - When creating new files/modules
- `/ai-rpi-protocol_project-info/glossary.md` - When naming variables, functions, classes
- `/ai-rpi-protocol_project-info/integrations.md` - When implementing external API calls
- `/ai-rpi-protocol_project-info/monitoring.md` - When adding logging, metrics (optional file)

## Loading Strategy

### 1. Essential Files (Load Early)
Load these at the start of each phase if they exist:
- **Phase R:** overview.md, constraints.md, custom-instructions.md
- **Phase P:** constraints.md, stack-patterns.md, custom-instructions.md
- **Phase I:** constraints.md, stack-patterns.md, standards.md, custom-instructions.md

### 2. Context-Sensitive Files (Load as Needed)
Load these only when the task requires them:
- **structure.md** >> When navigating codebase or creating new directories
- **glossary.md** >> When dealing with domain-specific terminology
- **integrations.md** >> When working with external APIs
- **monitoring.md** >> When adding observability features

### 3. Lazy Loading
Don't load all files at once. Load them when:
- You need specific information from that file
- The task scope expands to cover that area
- User mentions something related to that file's domain

## File Purpose Quick Reference

| File | Contains | When to Load |
|------|----------|-------------|
| `overview.md` | Project description, domain, tech stack | Phase R start |
| `constraints.md` | Non-negotiable rules, compliance | All phases (mandatory) |
| `structure.md` | Architecture, directories, entry points | When navigating/creating files |
| `stack-patterns.md` | Coding patterns, conventions | Phase P & I (mandatory) |
| `glossary.md` | Domain terminology, acronyms | When naming things |
| `standards.md` | Code style, testing, git practices | Phase I (mandatory) |
| `integrations.md` | External APIs, rate limits | When working with integrations |
| `monitoring.md` | Logging, metrics, observability | When adding monitoring (optional) |
| `custom-instructions.md` | User preferences, custom instructions | All phases (load when exists) |

## Token Conservation

**Don't load everything upfront.** This wastes tokens and adds noise.

**Good Example:**
```
User: "Add email validation to signup"

Phase R: Load overview.md, constraints.md
- Need to understand domain and any email rules

Phase P: Load constraints.md, stack-patterns.md
- Need rules and patterns for validation

Phase I: Load constraints.md, stack-patterns.md, standards.md
- Need rules, patterns, and code style
```

**Bad Example:**
```
User: "Add email validation to signup"

Load: ALL 8 project-info files upfront
- Wastes tokens on irrelevant files (integrations.md, monitoring.md)
- Adds noise to context
```

## Validation Check

Before proceeding to Phase R, verify:
1. ✅ Check if project-info files exist
2. ✅ If missing: Show welcome message Format A (ask to generate)
3. ✅ If exist: Load essential files for current phase
4. ✅ Load additional files only when relevant

## Example Workflows

### Example 1: Add New Feature
```
Task: "Add PayPal payment support"

Phase R:
- Load: overview.md (understand domain)
- Load: constraints.md (check compliance rules)
- Load: integrations.md (see existing payment patterns)

Phase P:
- Load: constraints.md (respect rules)
- Load: stack-patterns.md (follow patterns)
- Load: integrations.md (integration best practices)

Phase I:
- Load: constraints.md (enforce rules)
- Load: stack-patterns.md (code patterns)
- Load: standards.md (code style)
- Load: integrations.md (API patterns)
```

### Example 2: Fix Bug
```
Task: "Fix validation error on form"

Phase R:
- Load: overview.md (context)
- Load: constraints.md (any rules)
- Load: structure.md (find form files)

Phase P:
- Load: constraints.md (rules)
- Load: stack-patterns.md (validation patterns)

Phase I:
- Load: constraints.md (rules)
- Load: stack-patterns.md (patterns)
- Load: standards.md (code style)
```

### Example 3: Refactoring
```
Task: "Refactor authentication service"

Phase R:
- Load: overview.md (understand auth context)
- Load: constraints.md (security rules)
- Load: structure.md (current architecture)

Phase P:
- Load: constraints.md (security rules)
- Load: stack-patterns.md (patterns)
- Load: structure.md (architecture)

Phase I:
- Load: constraints.md (rules)
- Load: stack-patterns.md (patterns)
- Load: standards.md (code style)
- Load: structure.md (where to place files)
```

## Summary

**Load on demand, not upfront.** Each phase has essential files to load, plus context-sensitive files to load as needed. This conserves tokens and keeps context focused.
