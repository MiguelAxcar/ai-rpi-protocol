purpose: define AI-RPI's canonical contract plus adapters model; output: canonical source of truth, adapter philosophy, surface mapping, drift rules, and manifest guidance; use when: explaining how AI-RPI maps into modern agent surfaces.

# Canonical contract + adapters

AI-RPI defines one canonical contract and adapts it to modern agent surfaces, instead of duplicating truth everywhere.

This is a product principle, not just a documentation preference.

Core principles:
- **AI-RPI should be readable by humans first, adaptable by tools second.**
- **Do not turn the protocol into config. Use config only to support the protocol.**
- natural language carries intent, judgment, policy, trade-offs, and behavioral expectations
- structured metadata supports indexing, mapping, drift detection, and adapter behavior where that support is genuinely useful

## Why this model exists

Modern coding-agent ecosystems expose multiple tool-native surfaces:
- `AGENTS.md`
- `CLAUDE.md`
- `.claude/agents/*`
- `.github/agents/*.agent.md`
- skills
- subagents
- MCP-aware configuration surfaces
- editor and model adapter docs

Without a clear model, those surfaces drift into separate interpretations of AI-RPI.

That is a maintainability problem:
- users see inconsistent protocol behavior between tools
- adapters silently carry stale Mode, Depth, validation, or loading semantics
- new surfaces get added by copy-paste instead of alignment
- the repo accumulates duplicated truth that humans have to reconcile manually

AI-RPI should not solve that by turning the protocol into YAML. It should solve it by keeping one strong human-readable contract and making adapters thin, explicit, and aligned.

## Canonical source of truth

AI-RPI has **one canonical source of truth**.

That canonical source of truth is the human-readable natural-language contract defined across the core protocol docs, especially:
- `core/system/` for the system model and product architecture
- `core/phases/` for the public RPI spine and phase contracts
- `core/rules/` for always-on behavioral and operational rules

Supporting rule:
- adapter files, entry surfaces, skills, subagents, and tool-specific docs must align to that canonical contract rather than reinterpret it independently

Implication:
- `AGENTS.md`, `CLAUDE.md`, skills, subagents, and tool-specific surfaces are not equal parallel truths
- they are adapter or support surfaces that route into, expose, or operationalize the canonical contract

## Human-readable first

AI-RPI is intentionally written in natural language.

Why:
- policy needs judgment, not only keys and values
- behavioral rules need explanation, not only toggles
- trade-offs need reasoning, not only schema fields
- engineers need to edit the protocol directly without first becoming maintainers of a config compiler

Good use of natural language:
- policy
- reasoning
- judgment
- trade-offs
- behavioral expectations
- adapter philosophy

Bad use of structured metadata:
- encoding the full protocol as YAML or JSON
- duplicating full semantic meaning across every tool surface
- making machine-readable config more authoritative than the natural-language contract

## Adapter philosophy

AI-RPI should stay tool-agnostic at the contract level and tool-native at the adapter level.

Rules:
- keep the canonical contract tool-agnostic
- let adapters become richer where a tool supports richer behavior
- do not dumb AI-RPI down to the lowest common denominator
- do not fork AI-RPI semantics per tool unless truly necessary
- keep adapters thin where possible

Short version:
- **least common truth, richest adapter**
- canonical meaning stays stable
- adapters expose richer capability where the tool allows it

## Adapter surfaces

AI-RPI maps into multiple adapter surfaces. They do not all play the same role.

| Surface | Role | Desired duplication level | Notes |
|---------|------|---------------------------|-------|
| `AGENTS.md` | default repo-native entry adapter | low | detects level, routes into canonical docs, loads adapters |
| `CLAUDE.md` | Claude Code entry adapter | lowest | should stay a thin redirect or thin wrapper over `AGENTS.md` or the canonical contract |
| `.claude/agents/*` | Claude-native richer adapter surfaces | low to medium | may expose richer tool-native behavior, but should not fork canonical semantics |
| `.github/agents/*.agent.md` | GitHub custom agent adapter surfaces | low to medium | may package role-specific behavior for GitHub environments |
| skills | operational support surfaces | low | reusable workflows aligned to canonical contract |
| subagents | specialist worker surfaces | low | delegated workers aligned to canonical contract |
| IDE adapters | tool-native loading and behavior notes | low | explain how a tool should load and express the contract |
| model adapters | model-specific compliance notes | low | tighten behavior without redefining protocol semantics |
| MCP-aware config surfaces | capability and connection support | low | support how a tool reaches systems, not what AI-RPI means |

## Canonical vs adapters diagram

```text
human-readable canonical contract
  core/system/
  core/phases/
  core/rules/
        |
        v
  adapter entry surfaces and support layers
    -> AGENTS.md
    -> CLAUDE.md
    -> IDE adapters
    -> model adapters
    -> skills
    -> subagents
    -> .claude/agents/*
    -> .github/agents/*.agent.md
    -> MCP-aware config surfaces

supportive structure only
  -> optional light manifest for indexing, mapping, and drift checks
```

## What adapters should do

Good adapter behavior:
- expose the canonical contract through a tool-native surface
- add only the minimum tool-specific instructions needed for that surface
- reference canonical docs instead of copying them wholesale
- expose richer capabilities only where the tool genuinely supports them
- stay thin enough that drift is visible and fixable

Bad adapter behavior:
- silently forking the meaning of Mode, Depth, validation, or progressive loading
- embedding a second full version of AI-RPI inside the adapter
- carrying stale copies of canonical policy
- treating every surface as a self-contained equal truth

## Tool-specific overrides

Tool-specific overrides are allowed only where they are genuinely necessary.

Acceptable reasons:
- a tool has a unique loading mechanism
- a tool supports richer capabilities such as forked skills, custom agent files, or MCP tool routing
- a tool needs recovery instructions for its own failure modes
- a model family needs tighter compliance notes without changing protocol meaning

Unacceptable reasons:
- convenience copy-paste
- avoiding references to the canonical contract
- rephrasing the same policy independently in every adapter

## Adapter drift

Adapter drift is a real concept and a real maintainability problem.

Adapter drift means the canonical contract and one or more adapter surfaces no longer line up.

Examples:
- `AGENTS.md` says one thing while `CLAUDE.md` implies another
- one adapter reflects old Mode or Depth behavior
- one adapter omits progressive loading or validation rules that are now canonical
- one adapter adds tool-specific instructions that conflict with the canonical contract
- a skill or custom agent file operationalizes stale semantics after the canonical contract changed

Rules:
- drift should be surfaced
- drift should not be normalized as incidental messiness
- drift should be treated as a maintainability problem with user-facing consequences
- fixes should usually update the thinnest possible adapter layer or the canonical contract, depending on where the truth changed

### Adapter drift rule set

1. Check entry surfaces against the canonical contract when core semantics change.
2. Check IDE and model adapters when loading, validation, or interaction rules change.
3. Check skills and subagents when operational-unit semantics change.
4. Check richer tool-native surfaces when a tool exposes capabilities the canonical contract now models differently.
5. If drift is small, fix the adapter directly.
6. If multiple adapters drift together, update the canonical contract first, then realign adapters.
7. Do not solve drift by copying more protocol text into more places.

## Manual maintenance now, generation later

Adapters are **manually maintained files for now**.

That is the right default:
- it keeps the system understandable
- it avoids overclaiming a generation system that does not yet exist
- it keeps humans able to edit and review the real behavior directly

At the same time, adapters are **conceptually generatable later** if generation would reduce drift and maintenance cost.

Important:
- generation is a future path, not a current requirement
- the architecture should stay forward-looking without becoming implementation-heavy now

## Light machine-readable manifest

AI-RPI may eventually use a **light machine-readable manifest** as a support layer.

This manifest is not the protocol itself.

Its job would be to support the canonical contract, not replace it.

Good uses:
- adapter inventory
- file roles
- canonical-to-adapter mapping
- drift-sensitive areas
- future generation hints if they actually reduce maintenance cost

Bad uses:
- storing the full meaning of the protocol
- moving policy and judgment out of natural-language docs
- making structured metadata the primary authoring surface

### Recommended light manifest shape

Keep it light. For each adapter surface, a manifest could track fields such as:
- `name`
- `surface`
- `path`
- `status`: `manual` or `derived-later`
- `canonical_sections`
- `tool_specific_overrides`
- `drift_sensitive_areas`

Example direction:

```yaml
adapters:
  - name: agents-entry
    surface: AGENTS.md
    path: /AGENTS.md
    status: manual
    canonical_sections:
      - runtime-classification
      - level-selection
      - protocol-loading
    tool_specific_overrides:
      - repo-entry-behavior
    drift_sensitive_areas:
      - level-selection
      - adapter-loading
```

This is only a support layer. The natural-language contract remains primary.

## Practical examples

Good examples:
- canonical AI-RPI principles defined in the core contract and reflected into `AGENTS.md`
- Claude Code or GitHub custom agent surfaces exposing richer behavior while still mapping back to the same contract
- a drift check that catches an outdated adapter after Mode, Depth, or validation semantics changed
- a light manifest mapping canonical sections to adapter files without becoming the protocol itself

## Maintenance guidance

When changing AI-RPI:
1. change the canonical contract first
2. identify which adapter surfaces are affected
3. update only the surfaces that need alignment
4. check for adapter drift in the most sensitive areas
5. avoid duplicating more text than necessary

Success condition:
- one human-readable canonical contract
- multiple tool-native adapters
- thin duplication
- explicit drift handling
- structured support only where it reduces drift or improves adapter behavior