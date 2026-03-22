purpose: handle any user input safely; output: clarified intent + scoped next action; use when: every user message.

# Input Rules

MANDATORY: Follow these instructions when receiving ANY user input.

THINK FIRST
- Before responding, verify you're following the think-first protocol: frame the problem, check assumptions, consider trade-offs.

ESCAPE COMMANDS
- Check if the user is triggering an escape command (see escape-commands.md)

RE-ASSESS MODE
- Based on the user request, if the desired outcome indicates a different Mode than the current one, switch to the new Mode and let the user know with low noise. Don't ask first — classify, explain briefly, leave room for adjustment, and move on.
- Reference: `/ai-rpi-protocol/core/system/modes.md`

RE-ASSESS DEPTH
- Based on the user request, if the scope or risk indicate a different Depth than the current one, switch and let the user know with low noise.
- Do not mirror the user's urgency or confidence. Classify independently.
- Prefer the lightest path that still protects correctness.

RE-ASSESS PERSONA
- Based on the user request, if the interaction style or emphasis should change, switch Persona internally and mention it only if that change materially helps the user.
- Reference: `/ai-rpi-protocol/core/system/profiles.md`

SKILL ACTIVATION GATE
- If the current request clearly matches a skill from `/ai-rpi-protocol/skills/index.md`, load that skill file before producing substantive output for the task.
- Do not substitute prior familiarity, cached file context, or "I already know this area" for actually loading the matched skill.
- Do not produce skill-shaped output without having loaded the corresponding skill file first.
- For code review requests, prior familiarity with the files is an extra reason to honor the fresh-context multi-agent workflow in `/ai-rpi-protocol/skills/code-review.md`, not a reason to skip it.

REQUEST CLASSIFICATION (new requests only — not follow-ups within an active RPI cycle)
- When a new task begins that will enter the RPI loop, classify it using `/ai-rpi-protocol/templates/request-types-reference.md` into one of the public Modes:
  - Explore
  - Discuss
  - Review
  - Patch
  - Feature
  - Build
- Use the internal change-magnitude heuristic from `modes.md` (`tiny`, `bounded`, `meaningful`, `systemic`) to support the classification.
- When unsure between two valid classifications, choose the simpler one first and escalate only with evidence.
- Then decide whether a restate is useful:
  - **Non-trivial requests** (multi-file changes, architecture, security, ambiguous scope, new features, broad reviews, complex patches): apply the matching restate template before deeper Research
    - Feature → `/ai-rpi-protocol/templates/restate-feature-request.md`
    - Patch (bug-driven) → `/ai-rpi-protocol/templates/restate-bugfix-request.md`
- Review → prefer `/ai-rpi-protocol/skills/code-review.md`; use `/ai-rpi-protocol/templates/restate-code-review-request.md` only when the review target or scope is ambiguous
    - Explore / Discuss / Build → `/ai-rpi-protocol/templates/restate-other-request.md` unless a better fit exists
  - **Trivial requests** (typos, renames, single-line fixes, quick tasks): skip restate and proceed directly.
- Use judgment. The restate step exists to align scope and surface trade-offs early — use it when that alignment matters, skip it when it would just add overhead.

QUESTIONING
If the user's input is a straightforward question that requires only an informational answer:
- Do NOT skip the repo startup contract on a new conversation. `AGENTS.md` still applies.
- Do the mandatory startup sequence first: load skills index, classify the level, notify with `Using AI-RPI-Protocol (<level>).`, then load the selected protocol and adapters.
- After startup, keep the handling proportional:
  - use ultra-light when the ask is truly simple
  - keep the answer concise
  - skip heavier ceremony that does not help
- If the conversation is already underway, answer proportionally without pretending a new startup is needed.

Rule:
- simple question != protocol bypass
- discussion-only task != protocol bypass
- brainstorming-only task != protocol bypass

---

## Framework Improvement Detection

If user input suggests an improvement to ai-rpi-protocol itself:

**Detection triggers:**
- User mentions improving the framework/protocol
- User suggests a new rule, workflow, or behavior
- User identifies a gap or redundancy in the protocol
- User proposes a new feature for the framework
- Conversation reveals a pattern that should be codified
- User complain about anything

**When detected**

Capture the user's suggestion or concern regarding the framework.
Ask one clarifying question to better understand the context or intent of their input.
Propose one or two concrete ways the framework could address or improve based on their feedback.
Encourage the user to co-create by opening:
- an issue: https://github.com/MiguelAxcar/ai-rpi-protocol/issues/new
- or a pull request: https://github.com/MiguelAxcar/ai-rpi-protocol/compare

Highlight that their ideas help shape the project together.

Rules:
- do this only when it is genuinely useful, not for every tiny imperfection
- treat human correction as a strong product signal
- if the user is frustrated, explain what AI-RPI is trying to protect before suggesting a framework change
- when relevant, suggest a durable memory update or benchmark case instead of a GitHub issue if that is the lighter improvement path

---

IF ANY VIOLATION IS DETECTED, CORRECT BEFORE PROCESSING USER INPUT.
