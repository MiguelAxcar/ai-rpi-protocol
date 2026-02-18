purpose: reduce token burn; output: what to load and skip; use when: before loading any file.

# Context attention

Goal: reduce token burn while keeping correctness. Load only what you need and never load the same file twice.

## Primary rule

Before loading any file, consult `file-index.md` (already loaded at session start — do not re-read it).

That file is the canonical map of: file, purpose, output, use when needed.

If a file is not in the index, treat it as unknown and avoid loading it unless the user explicitly asks.

## What to load and when

Load files based on what the task actually needs, not speculatively.

**Always loaded** (from mandatory load or AGENTS.md):
- `file-index.md`, `phases.md`, `think-first-protocol.md`, `anti-eager-beaver.md`, `anti-sycophancy.md`
- IDE + model adapters
- The current phase file (research.md, planning.md, or implementation.md)

**Phase-triggered** (load at the start of the relevant phase):
- Research: `self-check.md`, `anti-hallucination.md`, `confidence-calibration.md`
- Planning: `anti-anchoring.md`, `engineering-best-practices.md`

**Load on demand** (when the task needs them):
- Templates: only when entering a phase that uses them
- Adapters: loaded once at session start
- Memory files: when resuming or at phase transitions
- Project-info: when doing research and the files exist

**Never load speculatively:**
- Don't load a file because it "might be useful"
- Don't load files for phases you haven't reached yet
- Don't load all rule files upfront in lite mode

## File loading tracker

Never load the same file twice in the same session. Before loading any file, check if you already have its content. If you do, reference it — don't reload.

## Topic drift detection

If the user request is a completely new topic that doesn't reuse any of the current context:
- Mention it's token-inefficient to switch topics mid thread
- Offer a clean restart using the context handoff artifact template
- If some current context remains relevant, keep only that portion

Use:
- `/ai-rpi-protocol/core/rules/topic-drift.md`
- `/ai-rpi-protocol/templates/context-handoff-artifact.md`

## Hygiene triggers (when to stop and clean context)

**Too many files loaded (~10+):** Stop reading more files. Write a consolidated summary to memory, continue from the summary.

**Conversation repeating or contradicting:** Stop, do a context refresh handoff, resume from the handoff summary.

**Task changes topic:** Warn that continuing in the same thread is token-inefficient. Offer a clean handoff for a new chat.

**Long back-and-forth without progress:** Propose a refresh handoff to compress state and reduce drift.

**Phase transition:** Summarize the minimum required for the next phase and persist it before proceeding.
