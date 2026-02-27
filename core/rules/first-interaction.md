purpose: first message behavior; output: welcome + state + next step; use when: first user interaction only.

## Auto-detect mode

Load modes list: `/ai-rpi-protocol/core/system/modes.md`

Pick exactly one mode based on what the user asked. Use the simplest mode that still manages the risk. If the request touches multiple files, core logic, data shape, security, payments, or deployments, bias toward a higher mode. Mode selection changes depth and rigor. It does not change the RPI phases unless the task is genuinely trivial or the user explicitly bypasses phases via escape commands. If the user asks to learn, asks "explain", asks for step by step, or you detect a knowledge gap that will likely cause rework, choose Teaching for example.

---

## Auto-detect profile

Load profiles list: `/ai-rpi-protocol/core/system/profiles.md`

Pick exactly one profile based on what the user asked. When in doubt, default to casual-pair. Pick the best fit using intent cues.

If multiple profiles match:
- prefer teacher when the user explicitly asks to learn ("teach me", "explain how to", "walk me through", "I want to understand", "show me step by step")
- prefer debugger over architect when the trigger is a bug or regression
- prefer optimizer over architect when metrics and performance are primary
- prefer consultant when high stakes wording and auditability matter
- prefer researcher when evidence is missing and assumptions are risky
- otherwise, default to casual-pair

---

## Memory system

Load memory handling: `/ai-rpi-protocol/core/rules/memory-handling.md`

Check if there's anything in memory. If memory exists, transparently inform the user of prior session data and summarize the relevant findings. Assess if the memory indicates an unfinished task or an open session.
- If the memory appears unrelated to the current request, briefly mention its existence and proceed; do not stop unless the user expresses interest.
- If the memory is relevant to the current task (unfinished work, open questions, or closely related tasks), present a concise MEMORY SUMMARY including completion state and what was found. Mention options to recover, clean, or archive (explain those).
- Evaluate if the memory content aligns with the current user request — use any useful context found, otherwise continue normally.
- Always index/summarize memory and consider if it connects to the new request; only pause for explicit user choice if a clear continuation is possible.
- Proceed with the conversation unless the user requests to resume, clean, or archive past work.

Do all memory operations inside `/ai-rpi-protocol/memory`

---

## Welcome message

Check user preferences at `/ai-rpi-protocol/user-preferences/preferences.md` (if it exists).
Load welcome message template: `/ai-rpi-protocol/templates/welcome-message.md`

ASSESS BEST CASE

CASE A: welcome message was shown already to this user, given user preferences
THEN make Welcome Message more concise / summarized to show again

CASE B: welcome message wasn't yet displayed
THEN show a full version of Welcome Message, and store on a flag that Welcome Message was displayed already, so it will be displayed more concise next time

---

## Project info check

Check if `/ai-rpi-protocol_project-info/` files are found:

- `/ai-rpi-protocol_project-info/overview.md` - Understand what the project is, domain, tech stack
- `/ai-rpi-protocol_project-info/constraints.md` - Understand limitations and rules before researching
- `/ai-rpi-protocol_project-info/structure.md` - When navigating codebase to find relevant files
- `/ai-rpi-protocol_project-info/glossary.md` - When encountering domain terms you need to understand
- `/ai-rpi-protocol_project-info/integrations.md` - When research involves external APIs or services
- `/ai-rpi-protocol_project-info/monitoring.md` - When researching logging, metrics (optional file)
- `/ai-rpi-protocol_project-info/stack-patterns.md` - Follow established patterns in plan
- `/ai-rpi-protocol_project-info/standards.md` - When planning code structure or testing approach
- `/ai-rpi-protocol_project-info/custom-instructions.md` - User preferences and custom instructions (honor in all phases)

If found, a simple message telling that project info was found is enough, and you can move forward.

If project context files not found:
- Mention that project context files are missing and briefly explain why they help (better research, fewer wrong assumptions, more aligned suggestions)
- Continue with the user's request normally — do NOT block
- Remind the user periodically (not every message, use judgement) that generating project info would improve results. Say something like: "Project info is still missing — generating it would help me give better answers. Say 'generate project info' when you're ready."
- If the user says "generate project info", follow instructions in `/ai-rpi-protocol/core/project-info/generate-project-info-mode.md`

---
