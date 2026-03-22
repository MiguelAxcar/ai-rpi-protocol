purpose: define AI-RPI's setup lifecycle; output: bootstrap, health check, upgrade, setup profiles, ownership model, and version-awareness rules; use when: installing, adopting, upgrading, or checking protocol health.

# Setup lifecycle

AI-RPI should be easy to adopt, safe to upgrade, and cheap to keep healthy.

Core principles:
- bootstrap once
- generate project context once, then update it in place
- preserve project-owned context across protocol upgrades
- keep version awareness useful, not noisy
- surface health as actionable next steps, not warning theater

## Lifecycle stages

### 1. Bootstrap

Bootstrap is the first adoption step.

Goal:
- make AI-RPI runnable in the repo
- wire the correct entry surface
- establish durable project context when the team wants it

Bootstrap should create a usable baseline, not a permanent maintenance burden.

### 2. Health check

Health check is the lightweight ongoing check.

Goal:
- confirm the install still matches the intended setup profile
- detect missing or drifted setup surfaces
- recommend the smallest useful next step

Health check should be cheap, explicit, and low-noise.

### 3. Upgrade

Upgrade refreshes protocol-owned files while preserving project-owned context.

Goal:
- move the protocol forward in place
- keep durable project memory and preferences intact
- surface merge attention only where trust boundaries matter

Upgrade should not feel like reinstalling from scratch.

## Setup profiles

| Profile | Use when | Bootstrap result |
|---------|----------|------------------|
| **quick** | individual evaluation, low-friction adoption, or early trial | protocol folder installed, repo entry point wired, project-info optional |
| **standard** | normal day-to-day adoption | quick profile plus initial `/ai-rpi-protocol_project-info/` bootstrap with durable `memory.md` and `user-preferences.md` |
| **advanced-team** | shared team workflow, repeatable upgrades, clearer ownership | standard profile plus tracked install method such as subtree or submodule, explicit ownership expectations, and periodic health/upgrade rhythm |

Rules:
- quick is allowed to defer project-info generation
- standard is the default target for serious use
- advanced-team should prefer a tracked install method over copy-paste updates

## File ownership model

Setup trust depends on ownership being explicit.

| Surface | Ownership | Upgrade rule |
|---------|-----------|--------------|
| `/ai-rpi-protocol/**` | protocol-owned | may be upgraded in place |
| `/ai-rpi-protocol_project-info/**` | project-owned | preserve across upgrades; update in place, never wipe by default |
| repo-root `AGENTS.md` or `CLAUDE.md` | project-owned bridge file | keep aligned with protocol entry expectations, but do not clobber local project intent silently |
| `/ai-rpi-protocol/memory/**` session artifacts | runtime-owned | disposable and reconstructable; not a setup durability anchor |

Implications:
- protocol upgrades must not delete project-owned durable context
- generated project-info is created once, then maintained in place
- `memory.md` and `user-preferences.md` are durable anchors, not disposable generated fluff
- if a team edits protocol-owned files locally, upgrade behavior should surface drift instead of pretending the boundary does not exist

## Version awareness

Version awareness exists to support trust, not to create noise.

Use version signals when:
- bootstrap completes
- the user asks what version is installed
- a health check detects likely drift or stale setup
- an upgrade starts or finishes

Avoid version noise during normal task execution.

Practical rule:
- if the current work can proceed safely, do not interrupt it just to mention versions

Preferred version signals:
- `CHANGELOG.md` for human-readable release context
- the install method used by the repo, such as subtree, submodule, or direct copy
- visible local drift in protocol-owned files when it materially affects upgrade safety

## Bootstrap model

Minimum bootstrap surfaces:
1. install `/ai-rpi-protocol/`
2. wire the repo entry point the environment actually reads
3. choose a setup profile
4. optionally bootstrap `/ai-rpi-protocol_project-info/`

Recommended by profile:
- quick: install protocol folder plus entry point; start working immediately
- standard: quick plus bootstrap project-info, especially `memory.md` and `user-preferences.md`
- advanced-team: standard plus tracked install method, shared ownership expectations, and an upgrade path the team can repeat safely

## Health check model

Health check should answer a simple question: what is the smallest useful next step?

Check these surfaces:
1. Is the protocol folder present?
2. Is the correct root entry point wired?
3. Does the repo have the expected setup profile?
4. If project-info exists, are durable files preserved in place?
5. Is there visible drift in protocol-owned files that could complicate upgrade?
6. Is there a clear upgrade path for the chosen install method?

Suggested health outputs:

| Status | Meaning | Suggested next step |
|--------|---------|---------------------|
| **healthy** | setup matches the chosen profile | keep working |
| **bootstrap-needed** | required install surfaces are missing | complete the missing bootstrap step |
| **project-context-recommended** | protocol works, but durable project context is still absent | bootstrap or repair project-info when convenient |
| **upgrade-recommended** | setup works, but protocol version or structure is likely behind | perform an in-place upgrade |
| **merge-attention-required** | local edits on protocol-owned files may conflict with upgrade | review drift and merge deliberately |

Health checks should prefer recommendation language over breakage language unless the setup is actually unusable.

## Upgrade model

Upgrade should preserve trust by being predictable.

Default upgrade behavior:
1. detect the install method if possible
2. update `/ai-rpi-protocol/**` in place
3. preserve `/ai-rpi-protocol_project-info/**`
4. preserve project-owned bridge files unless the user chooses to realign them
5. run a health check view after upgrade

Project-info rules during upgrade:
- do not regenerate from scratch by default
- create missing durable files if the team wants the standard profile
- update generated project-info in place when repair is needed
- never silently erase `memory.md` or `user-preferences.md`

## Decision rule

Use the lightest lifecycle action that restores trust:

| Situation | Action |
|-----------|--------|
| protocol missing from repo | bootstrap |
| protocol present but entry point missing | bootstrap repair |
| protocol works, project-info absent, team still evaluating | stay quick or suggest standard |
| protocol works, durable context missing but repeat use is obvious | standard-profile bootstrap |
| protocol works, version is behind, no major drift | upgrade |
| protocol works, local protocol edits complicate replacement | drift-aware upgrade with merge attention |

The lifecycle is not install once and forget forever. It is bootstrap once, preserve trust, and upgrade safely.