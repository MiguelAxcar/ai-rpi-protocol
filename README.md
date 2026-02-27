# AI RPI Protocol

> A structured approach to AI assisted coding

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](./CHANGELOG.md)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

## TL;DR

Make AI code suggestions more reliable and less error prone in your IDE in 1 minute. This framework is a bunch of instructions finely tested and cured from hundreds of real engineering coding sessions, to make your AI coding assistant much smarter and assertive. In practice, this means some more tokens consumed but it pays off with *fewer wrong implementations, fewer rewrites, and better decisions earlier*. With you still in control. Benefits:
- AI doesn’t jump to code without understanding context
- Identifies assumptions, potential risks, and alternatives early
- Reduces rework and token waste, because correctness > speed
- Integrates with common IDEs and flows (Cursor, VS Code, Claude, etc)

## Quick install

1. Download or clone this repo into your project into `/ai-rpi-protocol`
2. Copy the entry point to your project root:
   - **Most IDEs** (Cursor, VS Code, Windsurf, Zed): `cp /ai-rpi-protocol/AGENTS.md ./AGENTS.md`
   - **Claude Code** (CLI or VS Code extension): `cp /ai-rpi-protocol/CLAUDE.md ./CLAUDE.md`
3. You keep prompting as usual. Under the hood, your AI assistant will now perform much better.

_**NOTE**: follow new releases and update it once a while._

## What AI RPI Protocol is

I spend quite a lot time stressing LLMs and AI coding assistants across engineering teams, building integrations and studying how they actually behave when you throw real pressure and real engineering problems on them. And what I found is not great.

RLHF training [literally reward the model for agreeing with you](https://aclanthology.org/2025.findings-emnlp.121.pdf), so it learn to say yes instead of what's correct. Anchoring bias make it lock into its first idea and dress up the rest as filler, so you think you're choosing but you're really just confirming. Hallucination make it reference APIs and methods that don't even exist, with the same confidence it cite real ones. An eager beaver reflex skip the thinking that would have caught the bad assumption before it became 200 lines of wrong code. Context drift in long sessions cause it to quietly forget its own instructions and start improvising. Even things like temperature, decoding strategies, and system prompt positioning affect instruction adherence in ways most engineers never think about. And
these aren't edge cases, this is how every AI coding assistant behave. You just don't always notice because the output look correct and the model never tell you when it's guessing.

This framework is what came out of that: drop some markdown files in your repo and your AI coding assistant goes from _"sure, here's 200 lines of JWT"_ to _"wait, what kind of auth do you actually need?"_

No new tools. No plugins. No config. Just markdown files, tuned from hundreds of real engineering sessions, telling what to enforce, what to skip, where AI needs a hard stop and where it just need a nudge. Every rule here exist because the opposite failed first.

You keep prompting as usual. Under the hood, your AI assistant will now:

- **Research first** — explores your codebase and surfaces what's actually true before proposing anything
- **Challenge weak ideas** — pushes back on vague requirements, hidden assumptions, and risky shortcuts instead of just agreeing. Won't just say yes because you sound confident
- **Show you real options** — presents genuinely different approaches with real trade-offs, not one good idea dressed up as three. Anti-anchoring rules make sure every option is actually worth picking
- **Display evidence** — references specific files and lines from your codebase, not vibes. If it can't prove something exist, it tells you instead of making it up
- **Calibrate confidence** — distinguishes what it verified from what it's guessing. You always know what to trust and what to double-check
- **Resists the urge to rush** — the eager-beaver reflex is real: the model is trained to help immediately, which usually mean skipping the thinking. This framework overrides that reflex
- **Enforces engineering best practices** — it will warn you if you try to store passwords in plain text, concatenate SQL strings, commit API keys to git, swallow exceptions silently, or skip tests on critical paths. It flags them before the code is even written. [Fully customizable](./core/rules/engineering-best-practices.md)
- **Stay transparent** — when the protocol influences a decision, the AI tells you what it did and why. No invisible guardrails

Think of it as an exoskeleton, not an autopilot: it reduce the cognitive load (search, recall, comparison) and expand visibility (assumptions, risks, trade-offs) but decisions and accountability stays with you, the engineer.

In practice, this means *fewer wrong implementations, fewer rewrites, and better decisions earlier*. With you still in control.

## _"But doesn't this use more tokens?"_

Yes. A bit more upfront. The assistant will research before coding, ask questions before assuming, and present options before writing code. That cost tokens.

But here's what I've seen over and over: the real token burn is not in thinking, but in rework. A wrong implementation that need to be debugged, reverted, replanned, rebuilt from scratch costs way more than spending a few extra tokens getting it right the first time.

Most of the token waste I see in AI assisted coding come from solving the wrong problem fast. The assistant jumps to code, the engineer accepts it because it looks right, and three rounds later they're still fixing the same problem. That's expensive, in tokens, in time, and in trust.

This framework front-loads the thinking (without outsourcing it) so you spend tokens on correctness instead of on rework. In practice, it tends to break even or save tokens on anything non-trivial, because you stop going in circles.

## More about problems this framework expect to solve

AI coding assistants tend to:

- **Jump-to-code behavior** - ask "how do I handle auth?" and get 200 lines of JWT before anyone asks what kind of auth you need
- **Yes-machine responses** - "_store passwords in localStorage_" >> "_great idea, here's how_". [Research shows](https://aclanthology.org/2025.findings-emnlp.121.pdf) RLHF amplifies sycophancy
- **Confident wrongness** - "_this regex handles all email formats_" (**no it doesn't**), "_this is thread-safe_" (**no it isn't**), "_this regex can parse HTML_" ([you can't parse HTML with regex!](https://stackoverflow.com/a/1732454))
- **Vibe coding** - code that looks right but doesn't handle edge cases, follows patterns, or considers scale
- **Scope creep disguised as help** - ask to fix a button and get a full component refactor you didn't ask for, with new abstractions and renamed files
- **Copy-paste architecture** - AI grabs a pattern from Stack Overflow or its training data and drops it in, ignoring that your codebase already has conventions in place
- **Silent assumption filling** - you leave a detail ambiguous and instead of asking AI picks the worst default and builds on top of it
- **Amnesia across turns** - AI forgets what it just researched two messages ago and starts contradicting its own findings - context handling
- **Hallucinated confidence** - "_the API supports batch mode_" (**it doesn't**), "_this library handles that natively_" (**there's no such method**), "_this is the recommended approach_" (**recommended by whom?**)
- **Zero trade-off answers** - every suggestion sounds perfect with no downsides mentioned. No complexity cost, no performance impact, no maintenance burden - just "_here's the solution_"

## What this is NOT

- **Not a new tool to learn** - it's markdown files that live in your repo
- **Not rigid** - escape commands let you bypass it anytime (`ignore framework`, `just do it`)
- **Not a replacement for your IDE** - it works alongside VS Code, Cursor, Claude Code, Zed, Windsurf, and others
- **Not a guarantee** - this protocol relies on AI voluntarily following instructions. LLMs can and _will ignore_ parts of it, specially in long conversations or with certain model/IDE combinations. It improves behavior, it doesn't control it

## Installation

### Quick install

1. Download or clone this repo into your project into `/ai-rpi-protocol`
2. Copy the entry point to your project root:
   - **Most IDEs** (Cursor, VS Code, Windsurf, Zed): `cp /ai-rpi-protocol/AGENTS.md ./AGENTS.md`
   - **Claude Code** (CLI or VS Code extension): `cp /ai-rpi-protocol/CLAUDE.md ./CLAUDE.md`
3. Start coding - the AI should follow the RPI workflow automatically

Lite mode is the default. See [Modes](#operation-modes) for configuration.

### Install using `git subtree` (recommended for teams, to get updates faster)

```
git subtree add --prefix=ai-rpi-protocol https://github.com/MiguelAxcar/ai-rpi-protocol.git main --squash
```

Update later:

```
git subtree pull --prefix=ai-rpi-protocol https://github.com/MiguelAxcar/ai-rpi-protocol.git main --squash
```

### Install using `git submodule`

```
git submodule add https://github.com/MiguelAxcar/ai-rpi-protocol.git ai-rpi-protocol
```

Then copy the entry point to your project root (see step 2 above).

## How it works

**Research >> Plan >> Implement** with approval gates at each step.

```
Phase 1: RESEARCH
├── AI explores, you review
├── Evidence-based findings (file:line refs)
└── Checkpoint: "Does this match? [yes/no]"

        (then)

Phase 2: PLANNING
├── AI proposes 2-3 approaches with trade-offs
├── You choose the best path
└── Checkpoint: "Ready to implement? [yes/no]"

         (then)

Phase 3: IMPLEMENTATION
├── AI follows approved plan exactly
└── Output: working code + tests
```

### Lite mode vs Full mode

Two loading modes, configured in your project root `AGENTS.md`:

- **Lite** (default) - loads phases, philosophy, self-check, and adapters. Everything else on-demand via file index
- **Full** - loads all rules, templates, memory, and compliance checks upfront

Change `mode: lite` to `mode: full` in your `AGENTS.md` to switch.

## Design decisions

| Decision | Rationale |
|----------|-----------|
| Research before coding | Understanding prevents wrong solutions |
| Options, not conclusions | There are no final solutions, only trade-offs; decisions belong to the engineer |
| Positive friction in decisions | Challenge weak requirements and hidden assumptions to help the engineer see further |
| Friction belongs in the system | Cognitive friction at decisions, trade-offs, side-effects, long-term approaches |
| Humans approve before AI implements | The engineer is accountable for what ships |
| Evidence over summaries | File paths and line numbers, not vague descriptions |

## Not sure if it's working?

Check the [compliance checklist](./core/rules/compliance-checklist.md) - observable green/red flags with recovery actions.

## Features

### Governance
- **RPI phases** - Research >> Plan >> Implement with explicit gates between each phase
- **Hard gates** - no phase advancement without explicit user confirmation
- **Positive friction** - challenges weak requirements and hidden assumptions, surfaces trade-offs, downstream impact, maintenance cost, and alternatives
- **Anti-sycophancy** - push back on risky approaches, present risks and side effects
- **Think-first** - structured reasoning before code. Resists the urge to help immediately
- **Anti eager-beaver** - treats the impulse to act fast as a trigger to stop and follow instructions. The model is trained to help immediately; this rule override that reflex
- **Evidence-based** - file paths and line numbers, not vague references. Assumptions marked explicitly
- **Transparency** - when the protocol influence a decision, the AI tell you what happened and why. Visible guardrails build trust
- **Engineering best practices** - enforces OWASP Top 10, SOLID, ACID, proper error handling, and other well-known standards by default. The AI suggest, you decide. Fully customizable — add or remove what make sense for your project
- **Anti-hallucination** - verifies references before citing them. If the AI can't prove it exist, it say so instead of making things up
- **Confidence calibration** - distinguishes verified facts from guesses. The engineer always know what to trust and what to double-check
- **Anti-anchoring** - prevents fake options. Every alternative must be genuinely viable, not a straw man to make the first idea look good

### Operation modes
- **Lite** (default) - loads phases, philosophy, self-check, and adapters. Everything else on-demand via file index
- **Full** - loads all rules, templates, memory, and compliance checks upfront
- **Operation levels** - Quick, Streamlined, Thoughtful, Comprehensive. Auto-detected, user-adjustable
- **Escape commands** - `skip`, `quick`, `just do it`, `ignore framework`

### Memory and context
- **Session memory** - `decisions.md`, `research-cache.md`, `plans/` persists across phases
- **Silent memory handling** - manages memory behind the scenes, reconstructs if missed
- **Context attention** - load only what you need, never load the same file twice
- **Topic drift handling** - detect conversation drift, offers clean handoff
- **Token discipline** - spend tokens on correctness, not narration. Artifacts in memory, lean summaries in chat

### Adapters
- **IDE** - VS Code, Cursor, Claude Code, Zed, Windsurf
- **Model** - Claude, GPT, Gemini, Grok, DeepSeek, local models
- **Profiles** - casual-pair, architect, consultant, researcher, mentor, teacher, optimizer, debugger

### Compliance
- **Self-check** - violation check before every output
- **Compliance checklist** - observable green/red flags with recovery actions. See [`compliance-checklist.md`](./core/rules/compliance-checklist.md)
- **Recovery commands** - `"stop - load ai-rpi-protocol"`, `"halt - you skipped the protocol"`

## Project info

A set of markdown files that captures stable truths about your project (domain terms, constraints, structure, coding patterns). Generated once, committed to the repo, reused across tasks.

**Location:** `/ai-rpi-protocol_project-info/` (outside the framework folder so updates don't overwrite your context)

**Generate:** Ask your assistant `Generate my project info`. It creates: `overview.md`, `constraints.md`, `structure.md`, `stack-patterns.md`, `glossary.md`, `standards.md`. Optional: `integrations.md`, `monitoring.md`.

## Known limitations

This protocol relies on AI voluntarily following markdown instructions. LLMs are not deterministic rule-followers - they can and will ignore, partially follow, or silently drop instructions, specially in long conversations or when the model's training biases push toward different behavior.

**Common reasons for non-compliance:**
- Trained to be "helpful" (immediate action feels helpful to the model)
- Some IDEs/models don't fully read custom instruction files
- Long conversations cause context drift
- Some models sometimes actively reject behavioral instructions

**Recovery commands:**
```
"stop - load ai-rpi-protocol"
"wait - follow AGENTS.md"
"halt - you skipped the protocol"
```

**User override:** `"ignore framework"` and the AI will comply. The framework is a tool, not a cage.

**Best results so far:** Cursor + Anthropic models.

## Contributing

Early project. Works for my workflows, needs testing across more IDEs and models.

Where contributions help most:
- **Adapter coverage** - IDEs, models, edge cases. Even a one-line fix helps
- **Real-world walkthroughs** - before/after with a real repo. Most impactful contribution right now
- **Testing reports** - what IDE, what model, what worked, what broke
- **Failure cases** - when the protocol doesn't work, document what happened and how you recovered
- **Docs** - if something is confusing, clarify

Also an open question from [Jake Nations](https://youtu.be/eIoohUmYpGI): "Will we still understand our own systems when AI is writing most of our code?"

[Open a PR](https://github.com/MiguelAxcar/ai-rpi-protocol/pulls) or [start a discussion](https://github.com/MiguelAxcar/ai-rpi-protocol/issues).

## License

MIT - [LICENSE](./LICENSE)

v1.0.0 - [CHANGELOG](./CHANGELOG.md)
