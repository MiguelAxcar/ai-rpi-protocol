purpose: define skills and subagents as AI-RPI operational units; output: distinction, inventories, mappings, loading policy, and transparency rules; use when: skills, subagents, delegation, challenge, or review behavior materially matter.

# Operational units

AI-RPI is not one giant monolithic workflow. It stays grounded in the public Research -> Plan -> Implement spine, while using a small set of operational units when the task proves they add leverage.

Core distinction:
- **Skills** = reusable procedural know-how / reusable workflows
- **Subagents** = specialist delegated workers with fresh context

Mental model:
- a **skill** is how to do a kind of work
- a **subagent** is who to delegate a kind of work to

This distinction is intentional. Do not blur it.

## Why this stays lightweight

AI-RPI deliberately prefers a **small, strong core skill set** over dozens of micro-skills, and a **small, clearly specialized subagent set** over spawning workers just because a phase exists.

Rules:
- do not preload all skills
- do not spawn subagents by default
- do not treat delegation as a ritual
- use the minimum useful operational units first
- widen only when Mode, Depth, phase, and evidence justify it

## Skills

Skills are reusable workflows. They sharpen judgment and execution by giving the assistant a reliable way to do a class of work.

Skills are for:
- reusable procedural know-how
- repeatable workflow structure
- proportionate outputs
- keeping good practice consistent across tasks

Skills are not for:
- forcing delegation
- replacing the public RPI spine
- loading every workflow up front
- creating a separate mini-protocol for every tiny task shape

### Core skill set

| Skill | What it is for | Use when | Do not use when |
|------|-----------------|----------|-----------------|
| `clarify-task` | sharpen vague asks, identify constraints, align on success | scope is fuzzy, requirements are partial, drift is likely | the task is already crisp and mechanical |
| `research-codebase` | inspect relevant files, patterns, architecture, dependencies, and evidence | the next decision depends on repo truth | the answer is already verified and local |
| `challenge-plan` | expose weak assumptions, hidden trade-offs, overengineering, and drift | the approach needs stress testing | there is no real plan or trade-off to challenge yet |
| `implement-change` | execute bounded work safely and incrementally | approved work needs to be carried out | the task should stop at research or planning |
| `verify-change` | produce validation evidence against intent, behavior, and acceptance anchors | code or config changed, or a review needs technical validation evidence | nothing materially changed and no validation question exists |
| `package-reviewable-work` | produce reviewer-ready summaries, acceptance mapping, confidence signals, handoff notes, PR narratives, and focus areas | the result needs to be reviewed, handed off, or explained | the task is so small that packaging would be noise |
| `review-code` | compatibility bridge for older review-code references | older docs still point here and need to be routed into `code-review` | any task that needs an actual review result |
| `write-tech-spec` | create proportional technical design artifacts | technical shape, migration, integration, or system behavior needs a durable artifact | a brief plan is enough |
| `write-prd` | create proportional product requirement artifacts | product intent, user outcomes, or cross-functional framing need a durable artifact | the work is purely technical or already well-scoped |

### Specialized workflow examples

The core set stays broad on purpose. Specialized workflows can still exist when they provide real leverage.

Current examples in this repo:
- `skills/automated-tests.md` -> a deeper workflow built mainly from `research-codebase`, `implement-change`, and `verify-change`
- `skills/code-review.md` -> the default strongest workflow for any explicit code review request

Those specialized workflows are examples, not the mental model the whole product should depend on.

## Subagents

Subagents are specialist delegated workers with fresh context. They exist to add perspective, isolation, or parallelism when that materially improves the outcome.

Subagents are for:
- fresh perspective
- context isolation
- specialist challenge or review
- parallel work when the task justifies it
- keeping the main thread focused

Subagents are not for:
- satisfying a rule that says every phase needs a worker
- duplicating the main thread without adding a new angle
- hiding weak reasoning behind orchestration
- widening context just because delegation is available

### Core subagent set

| Subagent | What it is for | Use when | Do not use when |
|---------|-----------------|----------|-----------------|
| `codebase-mapper` | map relevant code paths, modules, patterns, and impact surfaces | repo understanding is still incomplete | one or two local reads already answer the question |
| `challenger` | generalist positive-friction counterweight across phases | assumptions, trade-offs, or scope need independent pressure | there is nothing substantive to challenge |
| `architecture-reviewer` | challenge boundaries, interfaces, architectural fit, and long-term direction | changes cross boundaries or shape future structure | the change is purely local and architectural fit is obvious |
| `code-reviewer` | challenge correctness, maintainability, clarity, and reviewer readiness | a code review lens is needed | the task is still only clarifying or exploring |
| `debugger` | isolate likely root causes and failure paths | diagnosis is still unclear or regression paths are noisy | the issue is already understood and only needs implementation |
| `performance-reviewer` | inspect bottlenecks, efficiency, and scalability implications | performance could materially change or is already the concern | performance is irrelevant to the task |
| `security-reviewer` | inspect trust boundaries, misuse potential, and sensitive flows | auth, permissions, secrets, supply chain, or sensitive data are involved | the task is clearly outside meaningful security impact |
| `documentation-researcher` | look up current external docs, references, and library behavior | codebase evidence is insufficient and outside knowledge matters | the answer is already in the repo |
| `packaging-reviewer` | improve PR narrative, reviewer focus, and handoff quality | the outcome needs a stronger review package or handoff | the result is tiny and self-evident |

### Extended specialist set

| Subagent | What it is for | Use when | Do not use when |
|---------|-----------------|----------|-----------------|
| `web-researcher` | verify current external information (advisories, version behavior, deprecations) | recency-sensitive external facts matter to the decision | repo evidence already answers the question |
| `standards-discovery` | discover local conventions before planning/review/implementation | conventions are unclear but likely to influence quality | conventions are already known and loaded |
| `conventions-reviewer` | enforce architecture/module conventions from discovered standards | convention drift is a meaningful risk | the task is not a code review and no convention signal is needed |
| `patterns-reviewer` | evaluate naming/style/pattern consistency | style/pattern drift could harm maintainability | only hard correctness risk matters and style is out of scope |
| `test-quality-reviewer` | detect false-confidence tests and weak assertions | confidence depends heavily on tests in the diff | no tests changed and test confidence is not a decision factor |
| `documentation-reviewer` | detect docs-code divergence and rollout-doc gaps | behavior/interface change may desync docs | docs are unaffected and no public-facing behavior changed |

## Challenger pattern

The **challenger** is a first-class product feature.

The challenger is not just a spec critic. It is a strong generalist counterweight that can challenge across the lifecycle:
- vague asks
- weak requirements
- bad ideas
- unjustified assumptions
- hidden trade-offs
- likely side-effects
- scope drift
- architectural drift
- weak evidence
- false certainty
- unnecessary ceremony

The challenger exists to improve judgment, not block progress.

Use the challenger when it adds leverage:
- before a plan hardens
- when confidence seems too high for the evidence
- when the task has hidden cost or drift risk
- when a fresh critical pass is cheaper than rework later

Do not use the challenger just to create noise.

## Validation and review

Validation is the umbrella proving model. Review is one optional widening layer inside that model.

Validation can include:
- execution checks
- behavior validation
- acceptance mapping
- uncertainty reporting
- review lenses
- reviewer focus and packaging

Review is not one thing internally. AI-RPI can apply different review lenses when the task justifies them:
- correctness
- maintainability
- architecture fit
- product fit
- performance
- security
- reviewability and handoff quality

Not every task needs every lens.

Rules:
- keep validation evidence-based
- keep review proportional
- prefer the fewest useful lenses
- use specialist reviewers only when they add signal
- widen validation with criticality, user impact, blast radius, or uncertainty
- progressive loading still applies
- explicit code review requests still route to the strongest multi-agent review workflow rather than a lightweight verification pass

## Mode mapping

Mode is a strong recommendation signal for operational units. It should influence what is likely to help, but it should not blindly load everything.

| Mode | Preferred skills | Preferred subagents |
|------|------------------|---------------------|
| Explore | `clarify-task`, `research-codebase` | `codebase-mapper`, `debugger`, `standards-discovery`, `documentation-researcher`, `web-researcher` (when recency matters) |
| Discuss | `clarify-task`, `challenge-plan`, `write-tech-spec`, `write-prd` when justified | `challenger`, `architecture-reviewer`, `codebase-mapper`, `standards-discovery`, `documentation-researcher` |
| Review | `code-review`, `verify-change`, `package-reviewable-work` | `code-reviewer`, `architecture-reviewer`, `performance-reviewer`, `security-reviewer`, `packaging-reviewer`, plus `conventions-reviewer`, `patterns-reviewer`, `test-quality-reviewer`, `documentation-reviewer`, `challenger` as needed |
| Patch | `clarify-task`, `implement-change`, `verify-change`, `code-review` when a real review is warranted | `debugger`, `code-reviewer`, `challenger` when the patch has hidden trade-offs or thin validation evidence |
| Feature | `clarify-task`, `research-codebase`, `challenge-plan`, `implement-change`, `verify-change`, `package-reviewable-work`, shaping artifacts when justified | `codebase-mapper`, `standards-discovery`, `challenger`, `architecture-reviewer`, `code-reviewer`, risk-specific specialists |
| Build | broad combination of implementation, validation, packaging, and planning skills as justified | multiple specialists when evidence shows cross-cutting risk or review needs |

## Depth mapping

Depth controls how many skills load, whether subagents are justified, how much challenge is surfaced, and how layered review and packaging become.

### Minimal

- smallest useful skill set
- usually 1-2 skills active in practice
- subagents only when a fresh specialist view prevents obvious rework
- few review layers unless the task proves they matter
- validation can still escalate sharply if impact is high despite a small diff
- packaging should stay lean

### Balanced

- enough structure to protect correctness
- usually 2-4 skills active across the loop
- one focused subagent is normal when research, challenge, or review would otherwise sprawl
- challenge and review behavior should appear when it materially improves the result
- acceptance mapping and confidence should appear when implementation could look done while still missing intent
- packaging should help a reviewer quickly understand what changed and why

### Full

- stronger challenge and richer review layering
- broader skill combination when justified by task size and risk
- multiple specialist subagents are acceptable when they add real signal
- validation and packaging should be reviewer-grade, not just execution-grade
- do not widen just because full depth is available; keep it evidence-based

## Mode x Depth x skills and subagents matrix

| Mode | Minimal | Balanced | Full |
|------|---------|----------|------|
| Explore | Skills: `clarify-task`, `research-codebase` if needed. Subagents: usually none. | Skills: `clarify-task`, `research-codebase`. Subagents: `codebase-mapper`, `standards-discovery`, or `documentation-researcher` when local reading would sprawl. | Skills: `clarify-task`, `research-codebase`, `challenge-plan` when framing is weak. Subagents: `codebase-mapper`, `debugger`, `standards-discovery`, `documentation-researcher`, `web-researcher`, `challenger` as justified. |
| Discuss | Skills: `clarify-task`, `challenge-plan`. Subagents: usually none. | Skills: `clarify-task`, `challenge-plan`, planning artifact skill when needed. Subagents: `challenger`, sometimes `architecture-reviewer` or `codebase-mapper`. | Skills: `clarify-task`, `challenge-plan`, `write-tech-spec` or `write-prd` when justified. Subagents: `challenger`, `architecture-reviewer`, `codebase-mapper`, `standards-discovery`, `documentation-researcher`. |
| Review | Skills: `code-review`, `verify-change`, `package-reviewable-work`. Subagents: `code-reviewer`, `security-reviewer`, `architecture-reviewer` at minimum. | Skills: `code-review`, `verify-change`, `package-reviewable-work`. Subagents: `code-reviewer`, `security-reviewer`, `architecture-reviewer`, plus `conventions-reviewer`/`patterns-reviewer`/`test-quality-reviewer`/`documentation-reviewer` as justified. | Skills: `code-review`, `verify-change`, `package-reviewable-work`. Subagents: layered specialists including `code-reviewer`, `architecture-reviewer`, `performance-reviewer`, `security-reviewer`, `packaging-reviewer`, `conventions-reviewer`, `patterns-reviewer`, `test-quality-reviewer`, `documentation-reviewer`, `challenger` as justified. |
| Patch | Skills: `implement-change`, `verify-change` when needed. Subagents: usually none. | Skills: `clarify-task`, `implement-change`, `verify-change`. Subagents: `debugger` or `code-reviewer` when the patch has hidden uncertainty. | Skills: `clarify-task`, `research-codebase`, `challenge-plan`, `implement-change`, `verify-change`, `package-reviewable-work` as justified. Subagents: `debugger`, `challenger`, `code-reviewer`, plus risk-specific specialists. |
| Feature | Skills: rare, only for very small additive work. | Skills: `clarify-task`, `research-codebase`, `challenge-plan`, `implement-change`, `verify-change`, packaging when useful. Subagents: `codebase-mapper`, `challenger`, `architecture-reviewer` when boundaries matter. | Skills: broad combination of clarification, research, challenge, implementation, verification, packaging, and planning artifact skills as justified. Subagents: `codebase-mapper`, `challenger`, `architecture-reviewer`, `code-reviewer`, plus risk-specific specialists. |
| Build | Skills: rare except for tightly bounded execution work. | Skills: implementation, validation, packaging, and planning artifact skills as justified. Subagents: one focused specialist when the work would otherwise sprawl. | Skills: broad combination of implementation, validation, packaging, and planning skills. Subagents: multiple specialists when evidence shows cross-cutting risk, diagnosis, or layered review needs. |

## Progressive-loading compatibility

Skills and subagents must stay compatible with progressive loading.

Loading rules:
- Layer 3 = load only the skills the task clearly needs
- Layer 4 = spawn only the subagents that add fresh perspective, isolation, specialization, or parallel leverage
- do not load or spawn everything for a Mode
- let phase, evidence, and escalation triggers decide when to widen

Short loading policy:
1. Start with the smallest useful skill set.
2. Stay in the main thread while the next decision is still local and clear.
3. Use one subagent when fresh perspective or specialization clearly beats more local reading.
4. Add more validation, review, or challenge layers only when risk, uncertainty, criticality, or reviewer needs justify them.
5. Compact before widening again.

## Runtime transparency

When a skill or subagent materially influences the result, AI-RPI may say so briefly.

Good examples:
- `AI-RPI-Protocol brought in a review pass here because the change crosses boundaries.`
- `AI-RPI-Protocol used a challenge pass because the requirement had hidden trade-offs.`
- `AI-RPI-Protocol pulled in a debugger view because the failure path was still unclear.`

Rules:
- brief only
- useful only
- not every step
- high trust, low noise

## Recommended loading order

When skills or subagents matter:
1. load this file
2. identify the smallest useful skills for the current Mode and phase
3. decide whether the main thread can do the work cleanly
4. if not, delegate to the smallest useful subagent set
5. keep the engineer in control with proportionate transparency and gates
