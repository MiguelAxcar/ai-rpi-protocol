purpose: handle any user input safely; output: clarified intent + scoped next action; use when: every user message.

# Input Rules

MANDATORY: Follow these instructions when receiving ANY user input.

THINK FIRST
- Before responding, verify you're following the think-first protocol: frame the problem, check assumptions, consider trade-offs.

ESCAPE COMMANDS
- Check if the user is triggering an escape command (see escape-commands.md)

RE-ASSESS MODE
- Based on the user request, if the complexity/scope indicate a different mode than the current one, switch to the new mode and let user know, opening room for changing. Don't ask — change, mention the change, open room for change and move on.
- Reference: `/ai-rpi-protocol/core/system/modes.md`

RE-ASSESS PROFILE
- Based on the user request, if the complexity/scope indicates a different profile than the current one, switch and let user know, opening room for changing.
- Reference: `/ai-rpi-protocol/core/system/profiles.md`

REQUEST CLASSIFICATION (new requests only — not follow-ups within an active RPI cycle)
- When a new task begins that will enter the RPI phases, assess whether the request is worth restating:
  - **Non-trivial requests** (multi-file changes, architecture, security, ambiguous scope, new features, complex bugs): classify using `/ai-rpi-protocol/templates/request-types-reference.md` and apply the matching restate template before Phase R:
    - Feature → `/ai-rpi-protocol/templates/restate-feature-request.md`
    - Bugfix → `/ai-rpi-protocol/templates/restate-bugfix-request.md`
    - Other → `/ai-rpi-protocol/templates/restate-other-request.md`
  - **Trivial requests** (typos, renames, single-line fixes, quick tasks): skip restate and confirmation — proceed directly.
- Use judgement. The restate step exists to align scope and surface trade-offs early — use it when that alignment matters, skip it when it would just add overhead.

QUESTIONING
If the user's input is a straightforward question that requires only an informational answer (and does not require implementation, planning, or extended context), treat it as a standalone inquiry:
- Skip memory, context drift, RPI protocol phases, and request classification
- Assess whether research or fact-finding is needed to provide an accurate response
- Respond focusing only on the specific question asked

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

Capture the user's suggestion or concern regarding the framework. Ask one clarifying question to better understand the context or intent of their input. Propose one or two concrete ways the framework could address or improve based on their feedback. Encourage the user to co-create by opening an issue or pull request at https://github.com/MiguelAxcar/ai-rpi-protocol/issues/new, highlighting that their ideas help shape the project together.

---

IF ANY VIOLATION IS DETECTED, CORRECT BEFORE PROCESSING USER INPUT.
