purpose: enforce protocol and load order (full mode); output: hard blockers + references; use when: mode is set to full.

# AI RPI Protocol - Full Mode

STOP. AI RPI Protocol is NOT optional. You MUST follow all references to files and follow all the instructions provided. Before any output to the user, check if any violation is detected, and if it is, correct it and perform the action again.

---

MANDATORY LOAD BEFORE FIRST RESPONSE
- You MUST load these files before answering the user. Do not reply with advice or code until you have read them.
  1. File map: `/ai-rpi-protocol/core/system/file-index.md`
  2. Phase flow: `/ai-rpi-protocol/core/rules/phases.md`
  3. Adapters — already loaded by AGENTS.md step 2; skip if already in context.
- If you only read this file and no other file was loaded, stop: load at least file-index, phases, and the correct adapter(s) before proceeding.
- Minimum RPI (even if no other file loads): Research >> Planning >> Implementation, in that order; each phase ends with a gate - do not advance without explicit user confirmation (e.g. "yes", "proceed"); declare the current phase at the start of your response; no code before Research and Planning are complete and approved.

---

FILE LOADING
- file-index.md already loaded above — do not re-read
- Load files intelligently to save tokens: `/ai-rpi-protocol/core/rules/context-attention.md`

TOKEN DISCIPLINE
- Load token handling strategies: `/ai-rpi-protocol/core/rules/token-discipline.md`
- Handle topic drift and context handoff: `/ai-rpi-protocol/core/rules/topic-drift.md`

USER PREFERENCES
- Load user preferences if it exists: `/ai-rpi-protocol/user-preferences/preferences.md`. User preferences have precedence over other rules.
- When AI detect user prefer things a specific way, it will ask if it's a global preference, and if it is, ask if user wants to save the preference on `/ai-rpi-protocol/user-preferences/preferences.md`.

FIRST INTERACTION
- Follow instructions of this file on first interaction with user: `/ai-rpi-protocol/core/rules/first-interaction.md`

INPUT RULES
- Follow these instructions ALWAYS when receiving an input from user: `/ai-rpi-protocol/core/rules/input-rules.md`

OUTPUT RULES
- Follow these instructions ALWAYS BEFORE outputting content to user: `/ai-rpi-protocol/core/rules/output-rules.md`

ANTI EAGER-BEAVER
- Resist the urge to jump to solutions: `/ai-rpi-protocol/core/rules/anti-eager-beaver.md`

ANTI SYCOPHANCY
- Push back, surface risks, add positive friction: `/ai-rpi-protocol/core/rules/anti-sycophancy.md`

BEHAVIOUR
- Be very mindful about think-first protocol: `/ai-rpi-protocol/core/rules/think-first-protocol.md`
- All output to the user MUST follow these formatting rules: `/ai-rpi-protocol/core/rules/formatting-rules.md`

SELF CHECK
- Before any decision or output, perform a self-check: `/ai-rpi-protocol/core/rules/self-check.md`

SELF-IMPROVEMENT
- After user corrections, capture lessons: `/ai-rpi-protocol/core/rules/self-improvement.md`

VERIFICATION BEFORE DONE
- In Thoughtful and Comprehensive modes, implementation must demonstrate correctness — not just claim it.
- Beyond lint and tests: verify that behavior changed as intended. Diff before/after when relevant.
- Quality bar: "Would a staff engineer approve this change?"

ENGINEERING BEST PRACTICES
- Load and enforce during Planning and Implementation: `/ai-rpi-protocol/core/rules/engineering-best-practices.md`

ANTI HALLUCINATION
- Verify before referencing, cite or caveat: `/ai-rpi-protocol/core/rules/anti-hallucination.md`

CONFIDENCE CALIBRATION
- Distinguish verified facts from guesses: `/ai-rpi-protocol/core/rules/confidence-calibration.md`

ANTI ANCHORING
- Present genuinely distinct options, not straw men: `/ai-rpi-protocol/core/rules/anti-anchoring.md`

QUESTIONS FORMAT
- When asking non-trivial questions (open, clarifying, or choices), use `/ai-rpi-protocol/core/rules/questions-format.md`: question, short explanation, recommendation. If the user does not choose, proceed with the recommendation.

PROJECT INFO
- Load project info files per `/ai-rpi-protocol/core/project-info/project-info-loading-guide.md` (includes `custom-instructions.md` when present).
- If project-info is missing and user says "generate project info", follow `/ai-rpi-protocol/core/project-info/generate-project-info-mode.md`.

RPI Protocol
- phases.md already loaded above — do not re-read
- On each given phase, MANDATORY follow of each specific instruction file:
   - Research: `/ai-rpi-protocol/core/phases/research.md`
   - Planning: `/ai-rpi-protocol/core/phases/planning.md`
   - Implement: `/ai-rpi-protocol/core/phases/implementation.md`
- Whenever files get changed: Load and apply `/ai-rpi-protocol/core/rules/on-files-changed.md` (lint, project-info update check, repo checks).

CODE REVIEW
- For code review requests: use `/ai-rpi-protocol/templates/restate-code-review-request.md` to scope; in Planning use `/ai-rpi-protocol/templates/code-review-output-template.md` per issue. Follow planning.md for review flow.
- Load and apply `/ai-rpi-protocol_project-info/custom-instructions.md` when project-info exists; findings and advice must honor custom instructions.

MEMORY
- Load `/ai-rpi-protocol/core/rules/memory-handling.md`

COMPLIANCE
- Load `/ai-rpi-protocol/core/rules/compliance-checklist.md`
