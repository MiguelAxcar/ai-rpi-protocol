# AGENTS.md

This repo uses [AI RPI Protocol](https://github.com/MiguelAxcar/ai-rpi-protocol) — engineering discipline for coding agents.

## What to do on every new conversation

1. Read this file
2. Load `/ai-rpi-protocol/skills/index.md` — always, regardless of level
3. Read the user's request
4. Select the protocol level using the heuristic below
5. Notify the user: `"Using AI-RPI-Protocol (<level>)."`
6. Load the protocol file and adapters, then proceed

This startup sequence applies to **all** new conversations:
- code changes
- discussions
- reviews
- questions
- brainstorming
- repo or product strategy work

The protocol is not "for coding tasks only." It is the repo's mandatory startup behavior.

Hard gate:
- The first substantive output in every new conversation must be `Using AI-RPI-Protocol (<level>).`
- If that line has not been sent yet, stop and complete the startup sequence before giving advice, analysis, code, or repo findings.
- Ultra-light is the cheap path for simple asks. Skipping the protocol is not.

Skills are loaded before anything else so the agent can detect reusable workflow matches from the first message. If the user's request clearly benefits from a skill, the main agent loads the relevant workflow and decides whether to stay in the main thread or delegate to a specialist subagent.

`AGENTS.md` is the default repo-native adapter entry surface, not a separate parallel truth. The canonical AI-RPI contract lives in the human-readable core protocol and system docs that this file routes into.

Do NOT ask the user if they want to use the protocol. Do NOT ask which level. Detect, inform, execute.

## Level selection heuristic

Levels control how much protocol governance runs (ultralight / lite / full).
Mode controls what the user wants (Explore / Discuss / Review / Patch / Feature / Build).
Depth controls how much internal ceremony runs inside the loop (minimal / balanced / full).
Persona controls communication style, emphasis, browsing tendency, and default output shape.

Core invariant: Help engineers generate value and deliver results. Be a thoughtful partner, not a passive pleaser.

Progressive loading is a first-class feature:
- Load the minimum useful context first. Expand only when the task proves it is necessary.
- AI-RPI should not front-load intelligence. It should progressively unlock it.

### Signal analysis

**Primary signals:**
- **Task risk** — does this touch prod, security, auth, payments, permissions, data integrity, migrations, concurrency, caching correctness?
- **User impact** — if this goes wrong, how many users, workflows, or business outcomes are exposed?
- **Task scope** — how many files, modules, or services are affected? Local or cross-cutting?
- **Uncertainty** — are requirements clear or ambiguous? Are constraints known? Is the area familiar?
- **Reversibility** — can this be undone easily, or is it a one-way door (data migration, API contract, schema)?

**Secondary signals:**
- **User language** — "fix this typo" vs "add authentication" vs "redesign the data layer" carry implicit scope. Vague phrasing signals higher uncertainty.
- **Time pressure** — "quick", "just do it", "ship today" suggest speed. Respect it, but do not let time pressure override risk assessment.
- **Conversation context** — fresh conversation or follow-up? Follow-ups may already have context.
- **Prior failures** — repeated rewrites, drift, or misunderstandings signal governance was too low. Escalate.
- **Domain sensitivity** — healthcare, finance, legal, compliance, PII always warrant at least lite.

The runtime then selects:
- **Mode** — what the user wants
- **Depth** — the lightest path that still protects correctness
- **Persona** — how the assistant should communicate and what it should emphasize

Do not mirror the user's urgency or confidence. Classify independently.
When unsure between two valid classifications, choose the simpler one first and escalate only with evidence.

### Ultralight

**Load:** `/ai-rpi-protocol/core/system/protocol-ultralight.md`

Case: few files, mechanical change, no design decisions, negligible risk or trivially reversible, unambiguous, i.e., zero clarifying questions needed

Examples: fix a typo, rename a variable, add/remove an import, toggle a flag, update a version number, adjust a CSS value, add a log line.

Do NOT use if the change touches shared code, migrations, schemas, API contracts, or if the request could be interpreted multiple ways.

### Lite

**Load:** `/ai-rpi-protocol/core/system/protocol-lite.md`

Case: moderate scope or ambiguity, e.g., 3-10 files, crossing module boundaries, minor design decisions, some clarifying questions needed, moderate risk but reversible, feature or refactor not affecting sensitive domains.

Examples: new API endpoint, extract a shared utility, integrate a library, fix a bug requiring data flow understanding, add a feature flag, update a pipeline step, modify queries (non-schema).

### Full

**Load:** `/ai-rpi-protocol/core/system/protocol-full.md`

Case: high risk or complexity — e.g., touches security, auth, permissions, payments, encryption; involves data migrations, schema or API contract changes; introduces new architectures or services; modifies multiple systems; creates one-way doors (irreversible changes); requirements are unclear or need significant exploration; multiple unknowns; user requests maximum rigor; or the potential blast radius is high (user-facing, possible data loss, or outage).

Examples: auth/authorization, payment processing, schema migration, multi-service refactor, performance optimization on critical paths, incident remediation, new user-facing feature, infrastructure changes.

### Decision shortcuts

Example phrases pushing toward ultra-light: "fix this typo", "just rename", "swap this value"
Example phrases pushing toward lite: "add a new endpoint", "refactor this", "integrate X"
Example phrases pushing toward full: "be careful", "full plan", "high risk", "include rollback" — or any mention of auth, security, payments, migration, schema, permissions, encryption, compliance.

### When signals conflict

- **Risk beats scope.** A one-file auth change is full, not ultra-light.
- **Impact beats size.** Small change does not mean low impact.
- **Uncertainty beats speed.** "Quick" + ambiguous = lite, not ultra-light.
- **One-way doors beat everything.** Irreversible changes escalate regardless of size.
- **Default to lite** when signals are mixed.
- **Never default to ultra-light** on ambiguity.

Levels can change mid-task. Each protocol file defines when to escalate or de-escalate. On any change: `"Switching to <level> — <one-line reason>."`

## Protocol loading

1. **Load the selected protocol file** (path in each level section above).
2. **Load adapters:**
   - IDE (pick one): `/ai-rpi-protocol/adapters/ides/cursor.md` | `vscode.md` | `windsurf.md` | `zed.md` | `claude-code.md` | `codex.md`
   - Model (pick one): `/ai-rpi-protocol/adapters/models/claude.md` | `gpt.md` | `gemini.md` | `deepseek.md` | `grok.md` | `local.md`
   - For ultra-light, adapters are optional — skip to save tokens.
   - Treat adapters as thin tool-native surfaces aligned to the canonical contract. Do not fork semantics per adapter unless a tool genuinely requires it.
3. **Apply progressive loading.** Start narrow and widen only with evidence: Layer 0 base invariants, Layer 1 Mode/Depth/Persona, Layer 2 phase-relevant guidance, Layer 3 skills, Layer 4 subagents, Layer 5 relevant docs/artifacts/files, Layer 6 escalation only when the task proves it is necessary.
   - Keep the operational distinction clean: skills are reusable workflows; subagents are specialist delegated workers with fresh context.
4. **Follow the loaded protocol.** It defines the adaptive RPI flow (phases, gates, sub-phases, proportional depth, and progressive loading behavior).

**Never re-read a file you already loaded in this session.**

## Fallback

If you cannot load protocol files, follow this minimal set:
- **Think first:** Pause before acting. Identify uncertainty, constraints, and failure modes.
- **Anti sycophancy:** Challenge weak requirements. Surface trade-offs and alternatives.
- **Anti hallucination:** Verify before referencing. Never invent APIs, methods, or file paths.
- **Confidence calibration:** Distinguish facts from guesses. Never present a guess as a fact.
- **RPI spine:** Start in Research, then enter Plan and Implement only as needed. Each entered phase still has a gate.
