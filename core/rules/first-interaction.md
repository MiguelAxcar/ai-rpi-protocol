purpose: first message behavior; output: concise restatement + optional posture + next step; use when: first user interaction only.

## Auto-detect mode and depth

This file applies to every new conversation, including discussion-only, question-only, review-only, and brainstorming asks.

Startup rule:
- complete the `AGENTS.md` startup sequence before any substantive answer
- the first substantive output must be `Using AI-RPI-Protocol (<level>).`
- do not treat "simple question" as a reason to skip startup; use a lighter level instead

Before classifying Mode, Depth, or Persona, check persistent project context if it exists:
- `/ai-rpi-protocol_project-info/memory.md`
- `/ai-rpi-protocol_project-info/user-preferences.md`

These files should shape behavior early on every interaction.

If the project-info surface exists but `/ai-rpi-protocol_project-info/memory.md` is missing:
- create a minimal `memory.md` immediately
- treat that as silent repair, not as a blocker or a user decision
- continue startup normally

Load modes list: `/ai-rpi-protocol/core/system/modes.md`

Pick exactly one public **Mode** based on what the user wants. Use the simpler classification first when the request is ambiguous, then escalate only with evidence.

Pick exactly one public **Depth** based on what the work needs. Use the lightest depth that still manages the risk. If the request touches multiple files, core logic, data shape, security, payments, or deployments, bias toward higher depth. Depth selection changes rigor and artifact weight. It does not force every request through every RPI phase equally; Research/Inception decides whether the loop stops after Research, continues to Plan, or continues through Implement.

Do not mirror the user's urgency or confidence. Classify independently.

---

## Auto-detect persona

Load profiles list: `/ai-rpi-protocol/core/system/profiles.md`

Pick exactly one persona based on what the user asked. When in doubt, default to casual-pair. Pick the best fit using intent cues.

If multiple personas match:
- prefer teacher when the user explicitly asks to learn ("teach me", "explain how to", "walk me through", "I want to understand", "show me step by step")
- prefer debugger over architect when the trigger is a bug or regression
- prefer optimizer over architect when metrics and performance are primary
- prefer reviewer when the request is primarily inspection or audit
- prefer product-engineer when shaping value, delivery, or product trade-offs
- otherwise, default to casual-pair

Persona should stay mostly internal at runtime unless surfacing it clearly helps the user.

---

## Runtime transparency

On the first substantial interaction where classification materially matters:

- briefly surface selected **Mode** and **Depth** only if doing so helps the user understand the operating posture
- mention the initial progressive-loading posture only when it meaningfully affects the next step
- explain the choice in one short sentence
- make clear that the user is in control and can change either one

Preferred active signal:
- `This repo has AI-RPI-Protocol available - <one short concrete benefit>. Given the request of <short request shape>, I loaded only the essentials of AI-RPI-Protocol. We're currently on Mode <Mode> and the Protocol Depth is <Depth>.`

Rules:
- generate the benefit based on the current task and likely value
- describe the request shape in plain language the user would recognize
- do not rely on a fixed canned list
- do not mention internal layer numbers to the user

Use explicit flagging when the protocol intervenes:
- `AI-RPI flagging <what> - <why it matters>.`

If a skill or subagent materially shapes the result later, mention that briefly when it becomes relevant.

Do NOT force this onto trivial work, ongoing turns, or interactions where it adds no clarity.
Do NOT surface Persona by default.

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

Check project-scoped user preferences at `/ai-rpi-protocol_project-info/user-preferences.md` first if it exists.
Load welcome message template: `/ai-rpi-protocol/templates/welcome-message.md`

Use the welcome template as a shape, not a mandatory banner.

Rules:
- default to a concise opening
- use a fuller opening only when the task is non-trivial and the extra context genuinely helps
- do not repeat the same protocol explainer once the interaction is already underway
- avoid decorative headers, repeated capability lists, or phase walkthroughs unless they materially help

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
- `/ai-rpi-protocol_project-info/memory.md` - Durable project memory (load early on every interaction if present)
- `/ai-rpi-protocol_project-info/user-preferences.md` - Durable project-scoped user preferences (load early on every interaction if present)

If found, a simple brief acknowledgement is enough when it is relevant; otherwise just use it and move forward.

If project context files not found:
- Mention that project context files are missing only when it is relevant, and briefly explain why they help (better research, fewer wrong assumptions, more aligned suggestions)
- Continue with the user's request normally — do NOT block
- Remind the user occasionally, not routinely, that generating project info would improve results.
- If the user says "generate project info", follow instructions in `/ai-rpi-protocol/templates/project-info-generation/generate-project-info-mode.md`

If project-info exists but `memory.md` is the only missing durable file:
- repair `memory.md` silently and continue
- do not present the missing memory file as a red-path startup failure

---
