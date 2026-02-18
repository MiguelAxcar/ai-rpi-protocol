purpose: define subagent invocation; output: when and how to call subagents; use when: Research or task needs delegation.

# Subagent system

Some IDEs and AI tools support subagents — specialized tasks that run in a separate context and return results. This file describes when and how to use them within the RPI protocol.

## What subagents are

Subagents are focused research tasks that the AI delegates to a separate execution context (when the IDE supports it). They help keep the main conversation focused while doing deep investigation work.

Not all IDEs support subagents. If the current environment doesn't, do the research directly — the workflow is the same, just without the delegation.

## Available subagents

### 1. Codebase Researcher

**File:** `/ai-rpi-protocol/agents/codebase-researcher.md`

**Purpose:** Deep codebase investigation — find relevant files, trace execution flows, identify patterns.

**When to use:**
- User asks about existing code behavior
- Need to understand how a feature works before planning
- Looking for patterns to follow in implementation

### 2. Web Researcher

**File:** `/ai-rpi-protocol/agents/web-researcher.md`

**Purpose:** Search the web when codebase knowledge is insufficient.

**When to use:**
- Documentation for a library or API is needed
- Best practices for a specific technology
- Error messages that need external context
- Comparing libraries, approaches, or tools

**When NOT to use:**
- Questions answerable from the codebase (use Codebase Researcher)
- Questions the AI already knows confidently
- Opinion-based questions without factual answers

## How to invoke

1. Determine if a subagent would help (deep research that benefits from focused context)
2. Load the subagent file
3. Describe the task clearly: what to find, where to focus
4. Let the subagent work and return structured results
5. Use the findings in the current phase

If the IDE doesn't support subagents, follow the same research steps directly.

## Rules

- Only invoke when the research justifies it — not for simple file reads
- One subagent at a time unless the IDE supports parallel execution
- Use results immediately — don't invoke a subagent and then ignore its findings
- Subagent findings should include file:line references where possible

## Adding new subagents

1. Create file in `/ai-rpi-protocol/agents/[name].md`
2. Structure: purpose, when to invoke, steps, return format
3. Add to this guide and to `file-index.md`
