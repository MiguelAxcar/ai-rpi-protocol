purpose: keep progressive loading compact without reducing correctness; output: lean chat summaries + referenced memory artifacts; use when: every task, every phase, every response.

# Token discipline

Tokens are budget. Spend them on correctness (evidence, tests, clear decisions), not on narration, repetition, or reloading the same context.

This is the compaction half of progressive loading: once context has widened enough to answer the current question, condense it before widening again.

This file complements:
* /ai-rpi-protocol/core/rules/context-attention.md (what to load, and when)
* /ai-rpi-protocol/core/rules/memory-handling.md (what to write, and when)
* /ai-rpi-protocol/core/rules/topic-drift.md (how to handle context switches)

## Core rules

1. Prefer artifacts over chat
   * Write full artifacts to memory files.
   * In chat, show only a lean summary and point to the artifact location.
   * Recommend extra standalone markdown files only when they add real value, and ask before generating heavier shaping or delivery artifacts unless the user already asked for them.

2. Reuse before rework
   * Before researching or planning, read memory first.
   * If the answer exists in memory, reuse it and avoid re reading the codebase.

3. Avoid duplicate loading
   * Never load the same file twice in the same session.
   * If it is already loaded, reference it and continue.
   * If only partially loaded and more detail is needed, upgrade the load (do not restart from the top).

4. Load small, then upgrade
   * Start with the lowest cost signal (file purposes from the index, then targeted reads).
   * Upgrade to full file loads only when it changes a decision or prevents a mistake.

5. Compact locally before broadening again
   * After a broad search, subagent run, or multi-file read, condense the result into memory or a lean summary.
   * Do not carry raw exploration trails forward if the next decision only needs conclusions and evidence pointers.

6. Prefer targeted reads over broad scans
   * Read only the lines around the specific function, call site, or config.
   * Avoid dumping large code blocks. Quote only what is needed to support a claim.

7. Use subagents for expensive discovery
   * When codebase research would require reading many files, use `/ai-rpi-protocol/agents/codebase-mapper.md`.
   * The main agent should consume the research cache artifact, not the raw file reads.

8. Batch questions, reduce turn count
   * Ask the minimum number of questions needed to prevent wrong work.
   * Prefer one message with 2 to 4 well scoped questions over many small follow ups.
   * Use multiple choice when possible to compress the interaction.

## Default outputs by phase

Research
* Write: /ai-rpi-protocol/memory/research-cache.md (full findings, evidence)
* Chat: 3 to 7 bullets (what is true, key files, open questions), then checkpoint

Planning
* Write: /ai-rpi-protocol/memory/plans/{task}-plan.md (full plan, options, trade offs, tests)
* Write: {workspace_root}/artifacts/shaping/{date}-{artifact}.md when a shareable shaping artifact is approved
* Write: /ai-rpi-protocol/memory/decisions.md (decisions and why)
* Chat: 3 to 7 bullets (chosen option, key steps, major risks), then checkpoint

Implementation
* Chat: only meaningful progress (files changed, tests added, notable decisions)
* Avoid step by step narration unless the user asks for it
* Write: update /ai-rpi-protocol/memory/session-state.md at phase exit and append any decisions
* Write: {workspace_root}/artifacts/delivery/{date}-{artifact}.md when a delivery artifact should survive the session

## Evidence output rules

* Always prefer references (file:line or file:function) over long excerpts.
* If an excerpt is needed, keep it short and directly relevant.
* If evidence is not available, say so explicitly and explain the reasoning briefly.

## Token saving triggers

When any trigger fires, follow the "Context refresh handoff procedure" in:
* /ai-rpi-protocol/core/rules/memory-handling.md

Recommended triggers:
* Context has crossed the current Depth's soft budget
* 15+ exchanges on the same task
* The assistant start repeating itself, or the user asks the same thing twice
* The task scope expands into a different domain (topic drift)
* The plan or findings are too large to be useful in chat

When a trigger fires, compact first. Escalate Depth only if compaction alone would not preserve correctness.

## Topic drift

If the user asks for something that is not a substep of the current task, do not continue silently.

Follow:
* /ai-rpi-protocol/core/rules/topic-drift.md

## Minimal chat summary format

Use this format when linking to artifacts:

Saved:
* /ai-rpi-protocol/memory/research-cache.md (or /ai-rpi-protocol/memory/plans/{task}-plan.md)
* /ai-rpi-protocol/memory/decisions.md (if updated)

Summary:
* Point 1
* Point 2
* Point 3

Checkpoint:
* Does this match your understanding? (or) Ready to implement? (yes/no)
