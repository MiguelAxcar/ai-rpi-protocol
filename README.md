# AI RPI Protocol

> Make AI coding assistants instantly more reliable

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.1.0-green.svg)](./CHANGELOG.md)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

AI-RPI is a portable, repo-native workflow for coding agents.

You drop it into a repository, wire the entry surface your agent already reads, and the agent starts working with a stronger operating model: research before coding, challenge weak assumptions, adapt rigor to risk, validate before claiming done, and package results for the next human.

The goal is practical: fewer blind edits, fewer confident mistakes, cleaner reviews, and less rework.

Works across modern coding-agent workflows, including Codex, Claude Code, GitHub Copilot agents, Cursor, and similar repo-native environments.

## Why Teams Need This

Most AI coding failures are not syntax failures. They are reliability failures.

The agent moves too fast, assumes too much, agrees too easily, misses repo constraints, and produces plausible code before anyone has checked whether the framing was right. That is why small asks turn into rewrites, PR reviews turn into archaeology, and "fast" AI work burns tokens on repair loops instead of progress.

AI-RPI exists to make that behavior more reliable without turning everyday work into ceremony.

## What You Get

- **Research before code** so the agent looks at the repo before it starts freelancing
- **Challenge instead of yes-machine behavior** so weak ideas and missing constraints surface earlier
- **Adaptive rigor** so small fixes stay light and risky work gets more scrutiny
- **Validation before "done"** so passing prose is not mistaken for proof
- **Reviewable handoffs** so humans can quickly inspect what changed, what was verified, and what still needs attention

## Before And After

Without AI-RPI:

- ask for a PR review and get vague praise plus scattered nitpicks
- ask for a bug fix and get a cleanup campaign with weak grounding
- ask for a feature and get implementation before trade-offs are visible

With AI-RPI:

- the agent starts from Research and cites repo evidence
- the plan exposes trade-offs before implementation hardens
- validation and reviewer focus are part of the output, not an afterthought

## What It Is

AI-RPI is not trying to replace your model, IDE, CI, or engineering judgment. It gives those tools a clearer contract inside real repos.

## Try It In 60 Seconds

1. Add this repo to your project as `/ai-rpi-protocol`
2. Wire the root entry point your environment already respects:
   - **Most IDEs** (Cursor, VS Code, Windsurf, Zed): `cp /ai-rpi-protocol/AGENTS.md ./AGENTS.md`
   - **Claude Code** (CLI or VS Code extension): `cp /ai-rpi-protocol/CLAUDE.md ./CLAUDE.md`
3. Keep working in your normal environment

That is the quick profile. For bootstrap, health checks, upgrades, and team-oriented install methods, see [core/system/setup-lifecycle.md](./core/system/setup-lifecycle.md).

## Why It Converts Better Than Prompt Tweaks

Prompts help, but they reset too much work every session.

AI-RPI puts the workflow in the repo itself, so the discipline is portable, reviewable, and repeatable across sessions, people, and tools.

## Use It When

These are the five adoption scenarios AI-RPI is optimized to make clearer and safer:

1. **Understand a codebase or checkout flow**
   Ask the agent to trace a real flow. AI-RPI pushes it to inspect the repo first, map the path, cite evidence, and separate verified behavior from guesses.
2. **Review a colleague's PR**
   AI-RPI packages findings, confidence gaps, validation evidence, and reviewer focus instead of dumping an unstructured summary.
3. **Fix a small bug without over-ceremony**
   Narrow patches can stay narrow. The protocol still forces enough grounding to avoid the classic "tiny fix, surprising regression" pattern.
4. **Shape and implement a feature safely**
   The agent can explore options, surface trade-offs, and only then move into implementation with a reviewable execution path.
5. **Build a startup POC with discipline**
   You can move fast without fully dropping rigor: lighter artifacts, pragmatic defaults, and clearer founder, engineer, and stakeholder handoffs.

## What Changes After Install

Under the hood, your coding agent will now:

- **Start from Research** instead of guessing from the prompt alone
- **Challenge weak ideas** instead of acting like a yes-machine
- **Show real options** instead of fake alternatives around one preferred answer
- **Display evidence** with file paths and grounded repo context
- **Calibrate confidence** so verified facts and guesses do not sound the same
- **Adapt by mode and depth** so patches stay lean and risky work gets more scrutiny
- **Use deterministic guardrails** when the surface is risky enough that prose guidance is not sufficient
- **Package outcomes for humans** so engineers, reviewers, tech leads, PM-founders, and stakeholders get different kinds of summaries when they should

The point is practical: make AI coding assistants more reliable in the place that matters, your repo.

## Mini Case Studies

These are representative patterns from real coding-agent work, not vanity metrics.

### 1. Checkout-flow understanding

Without a protocol, "explain checkout" often becomes a shallow summary or a confident guess based on naming. With AI-RPI, the better outcome is a traced path: entry point, state transitions, pricing logic, failure paths, and explicit unknowns. That changes the follow-up conversation from "is this probably right?" to "which branch of the flow do we want to change?"

### 2. PR review that is actually reviewable

Unstructured AI review usually mixes nitpicks, speculation, and shallow praise. AI-RPI pushes review toward findings, evidence, confidence, and reviewer focus. The useful output is not "looks good overall". It is "here are the real risks, here is what was validated, and here is where a human reviewer should spend attention first."

### 3. Small bug fix without a mini rewrite

Agents often over-help. A small bug becomes a refactor because the model sees an opportunity to redesign. AI-RPI keeps bounded work bounded by default, but still forces enough repo grounding to avoid blind edits. That is the difference between a two-line fix and an unnecessary cleanup campaign.

### 4. Feature shaping before implementation drift

Feature work breaks when the agent starts coding before the trade-offs are visible. AI-RPI makes the agent clarify the scope, compare real approaches, and line up validation expectations before implementation hardens. That usually avoids the "technically correct, product-wrong" result.

### 5. Startup POC with cleaner founder handoffs

Startup teams often want speed and just enough rigor to stay sane. AI-RPI fits that mode well: lighter planning, stronger implementation discipline, and clearer packaging for founder updates, merge-readiness, and next-step ownership.

## Why AI-RPI Instead Of...

### Better prompts

Prompts are useful, but they reset too much work every time. AI-RPI encodes the workflow in the repo so the discipline survives across sessions, people, and tools.

### A prompt pack or instruction file only

Prompt packs help with wording. AI-RPI is broader: phase discipline, adaptive depth, validation model, guardrails, role-aware packaging, adapters, and memory handling.

### One vendor's agent workflow

Vendor-native workflows can be strong, but they are still vendor-native. AI-RPI is built to travel across repo-native surfaces without rewriting the whole operating model per IDE or model.

### Freeform vibe coding

Freeform prompting is great at feeling fast. It is much worse at staying grounded, reviewable, and transferable. AI-RPI is for teams that want AI help without betting quality on whoever typed the best prompt that day.

### Heavy process

This is not trying to turn every task into a PRD. The protocol is adaptive on purpose. Small tasks can stay light. Heavier artifacts and stricter controls are there when the work actually needs them.

## What This Repo Gives You

- A canonical human-readable contract for how coding agents should behave
- Thin adapters for repo-native entry surfaces such as `AGENTS.md` and `CLAUDE.md`
- Adaptive `Research -> Plan -> Implement` behavior with proportional depth
- Deterministic guardrails for risky and critical surfaces
- Persistent project context and project-scoped preferences
- Role-based collaboration for better handoffs and approval targeting
- Reviewable delivery patterns instead of raw chat transcripts

## Launch And Adoption Assets

If you want the repo positioned for sharing, see [docs/launch-kit.md](./docs/launch-kit.md). It includes repo description candidates, suggested tags, launch post drafts, an article outline, and a visual asset plan.

## What This Is Not

- **Not just another prompt pack** - it is built for disciplined coding-agent workflows, not prompt-only tactics
- **Not a sidecar chatbot workflow** - it plugs into the repo-native agent entry points and conventions your environment already uses
- **Not rigid** - it can stay light on small work and get stricter only when the risk justifies it
- **Not tied to one vendor** - the same harness can travel across Claude Code, Copilot, Cursor, Codex-style setups, and AGENTS-compatible environments
- **Not a model, IDE, or CI replacement** - it works with your existing model, editor, tests, review, and delivery systems
- **Not only for synchronous chat-driven work** - it also fits delegated agents, background workflows, and longer autonomous delivery loops
- **Not a replacement for engineering judgment** - it exists to encode discipline around agent behavior, not to take decisions away from engineers
- **Not a guarantee** - current coding agents can still ignore instructions, specially in long conversations or on weaker tool surfaces. AI-RPI improves behavior; it does not magically control it

## _"But Doesn't This Use More Tokens?"_

Usually a bit more up front.

But the real waste in agent work is rework: wrong implementation, shallow review, missing constraints, or three repair loops after a fast bad start. AI-RPI spends tokens earlier so you spend fewer tokens digging out of avoidable mistakes later.

## Problems It Is Designed To Reduce

Coding agents tend to:

- **Jump to code** before the repo reality is clear
- **Act like yes-machines** when the idea is risky or underspecified
- **Produce confident wrongness** with clean prose and weak evidence
- **Over-help** by expanding scope or refactoring unasked-for areas
- **Drop into vibe coding** where code looks plausible but does not fit the system
- **Forget context across turns** and start contradicting earlier findings
- **Hide trade-offs** behind a single overconfident answer

## Install Beyond The Quick Start

If you want a cleaner long-term setup, AI-RPI supports three adoption levels:

- **quick** — try it fast with the protocol folder and one root entry point
- **standard** — add durable project context with `memory.md` and `user-preferences.md`
- **advanced-team** — use subtree or submodule workflows for repeatable upgrades and shared ownership

The full install, upgrade, and ownership guidance lives in [core/system/setup-lifecycle.md](./core/system/setup-lifecycle.md).

## How It Works At A Glance

The public spine is still `Research -> Plan -> Implement`, but the runtime adapts to the task instead of forcing every request through the same amount of ceremony.

The strongest differentiators are:

- **Repo-native discipline** — the operating model lives in files the agent already reads
- **Adaptive RPI spine** — one public flow, lighter or heavier depending on the work
- **Progressive loading** — load only the context the task proves it needs
- **Deterministic guardrails** — stronger control on risky surfaces without making simple work bureaucratic
- **Persistent project context** — stable project memory and preferences survive sessions and upgrades
- **Validation plus reviewer focus** — prove the result and tell the next reviewer where attention matters most
- **Role-based packaging** — package outcomes differently for engineers, reviewers, tech leads, PM-founders, and stakeholders

If you want the deeper system docs, start here:

- [core/system/progressive-loading.md](./core/system/progressive-loading.md)
- [core/system/deterministic-guardrails.md](./core/system/deterministic-guardrails.md)
- [core/system/persistent-project-context.md](./core/system/persistent-project-context.md)
- [core/system/validation-model.md](./core/system/validation-model.md)
- [core/system/role-based-collaboration.md](./core/system/role-based-collaboration.md)
- [core/system/setup-lifecycle.md](./core/system/setup-lifecycle.md)

## Project Context

AI-RPI can bootstrap durable project context under `/ai-rpi-protocol_project-info/`, especially `memory.md` and `user-preferences.md`, so stable project knowledge survives across sessions and upgrades instead of living in chat history.

## Known Limitations

This harness still relies on current coding agents actually honoring repo instructions, skills, and adapter rules. LLMs are not deterministic rule-followers: they can ignore, partially follow, or silently drop instructions, especially in long conversations or on weaker tool surfaces.

Common reasons:

- models are rewarded for sounding helpful before they are grounded
- some IDEs or models do not fully load repo instruction surfaces
- long conversations create context drift
- some model and tool combinations simply comply less reliably than others

If an agent drifts, reload the repo entry surface or restart the session. For observable red flags and recovery guidance, see [core/rules/compliance-checklist.md](./core/rules/compliance-checklist.md).

## Contributing

Early project. It works well in the workflows I stress it with, but it still needs broader testing across IDEs, models, and coding-agent environments.

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
