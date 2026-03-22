purpose: file map and load order; output: list of path + purpose/output/use when; use when: always first or before loading any file.

/ai-rpi-protocol/core/system/protocol-full.md - purpose: enforce protocol and load order (full level); output: hard blockers + references; use when: level is set to full.
/ai-rpi-protocol/core/system/protocol-lite.md - purpose: lean protocol entry point (lite level); output: core files + on-demand loading; use when: level is set to lite or not set.
/ai-rpi-protocol/AGENTS.md - purpose: default repo-native adapter entry surface; detect level, choose Mode/Depth/Persona, and route into the canonical protocol; output: protocol loading; use when: every new conversation.
/ai-rpi-protocol/CLAUDE.md - purpose: Claude Code adapter entry surface; output: thin routing into AGENTS.md and the canonical protocol; use when: Claude Code CLI or VS Code extension.
/ai-rpi-protocol/README.md - purpose: project intro and setup; output: what RPI is and how to install; use when: onboarding or reference.
/ai-rpi-protocol/CHANGELOG.md - purpose: version history; output: notable changes; use when: checking releases or version.
/ai-rpi-protocol/CONTRIBUTING.md - purpose: how to contribute; output: contribution guidelines; use when: contributing or PRs.
/ai-rpi-protocol/WISHLIST.md - purpose: future improvements; output: wishlist items; use when: planning features or roadmap.
/ai-rpi-protocol/METRICS.md - purpose: how to measure protocol effectiveness; output: what to track and when to adjust; use when: evaluating protocol value.

/ai-rpi-protocol/core/system/file-index.md - purpose: file map and load order; output: list of path + purpose/output/use when; use when: always first or before loading any file.
/ai-rpi-protocol/core/system/modes.md - purpose: define Mode and Depth selection; output: mode choice + depth choice; use when: start of request or re-assess.
/ai-rpi-protocol/core/system/profiles.md - purpose: define Persona selection rules; output: persona choice and style; use when: start of request or re-assess.
/ai-rpi-protocol/core/system/progressive-loading.md - purpose: define the progressive loading architecture; output: layers, budgets, triggers, compaction, and transparency; use when: before widening context beyond entry files.
/ai-rpi-protocol/core/system/operational-units.md - purpose: define skills and subagents as the protocol's operational units; output: distinction, inventories, mappings, loading policy, and transparency; use when: delegation, challenge, layered review, or workflow selection materially matter.
/ai-rpi-protocol/core/system/validation-model.md - purpose: define validation as the protocol's proving model; output: validation layers, review distinction, confidence rules, uncertainty handling, acceptance mapping, and escalation triggers; use when: implementation, review, confidence, or done-ness materially matter.
/ai-rpi-protocol/core/system/artifact-ladder.md - purpose: define the artifact ladder as the protocol's proportional artifact model; output: shaping vs delivery ladders, recommendation behavior, relationships, drift rules, and naming guidance; use when: planning, packaging, or artifact generation materially matter.
/ai-rpi-protocol/core/system/canonical-contract-adapters.md - purpose: define AI-RPI's canonical contract plus adapters model; output: canonical source of truth, adapter philosophy, surface mapping, drift rules, and manifest guidance; use when: explaining how AI-RPI maps into modern agent surfaces.
/ai-rpi-protocol/core/system/deterministic-guardrails.md - purpose: define AI-RPI's deterministic guardrails layer; output: soft-vs-hard control model, confirmation classes, trigger matrix, hook points, permissions posture, escalation classes, and runtime transparency rules; use when: risky or critical work needs stronger operational discipline than prose alone.
/ai-rpi-protocol/core/system/evaluation-flywheel.md - purpose: define AI-RPI's evaluation flywheel; output: task-success vs protocol-quality model, lightweight observability posture, failure taxonomy, correction signals, improvement loop, and benchmark guidance; use when: improving AI-RPI deliberately without adding analytics theater or noisy bureaucracy.
/ai-rpi-protocol/core/system/persistent-project-context.md - purpose: define durable project memory and project-scoped preference handling; output: loading order, capture rules, drift handling, and upgrade durability; use when: stable project context and preferences must survive across sessions and protocol upgrades.
/ai-rpi-protocol/core/system/setup-lifecycle.md - purpose: define setup lifecycle; output: bootstrap, health check, upgrade, profiles, ownership, and version-awareness guidance; use when: installing, adopting, upgrading, or checking protocol health.
/ai-rpi-protocol/core/system/role-based-collaboration.md - purpose: define the human role layer for collaboration; output: role selection, role-aware packaging, handoff routing, and approval boundary defaults; use when: human collaboration target, handoff, approval, or role-aware packaging materially matter.
/ai-rpi-protocol/core/system/protocol-ultralight.md - purpose: self-contained protocol for trivial tasks; output: better thinking without ceremony; use when: level is ultra-light.
/ai-rpi-protocol/core/system/subagent-system.md - purpose: define subagent invocation; output: when and how to call subagents proportionally; use when: a specialist delegated worker may add leverage.

/ai-rpi-protocol/skills/index.md - purpose: skills registry and operating model; output: core skill set, selection rules, and specialized examples; use when: every conversation (loaded from AGENTS.md).
/ai-rpi-protocol/skills/clarify-task.md - purpose: sharpen vague asks, constraints, and success criteria; output: scoped task framing; use when: request is ambiguous, underspecified, or drifting.
/ai-rpi-protocol/skills/research-codebase.md - purpose: inspect relevant repo truth before decisions; output: targeted findings with evidence; use when: the next decision depends on codebase reality.
/ai-rpi-protocol/skills/challenge-plan.md - purpose: stress-test a direction before or during planning; output: trade-offs, risks, drift warnings, and alternatives; use when: the plan needs deliberate challenge.
/ai-rpi-protocol/skills/implement-change.md - purpose: execute bounded approved work safely and incrementally; output: changes aligned to plan and repo patterns; use when: implementation is approved and needed.
/ai-rpi-protocol/skills/verify-change.md - purpose: produce technical validation evidence against intent and behavior; output: validation findings, confidence, and gaps; use when: code changed or a review needs technical confirmation.
/ai-rpi-protocol/skills/package-reviewable-work.md - purpose: produce proportional delivery artifacts for review and handoff; output: PR description, review package, handoff note, validation summary, diagram, or related delivery artifact; use when: the outcome needs clean review or transfer.
/ai-rpi-protocol/skills/review-code.md - purpose: compatibility bridge for older review-code references; output: routing into the full Code Review workflow; use when: older docs or flows still reference review-code.
/ai-rpi-protocol/skills/write-tech-spec.md - purpose: create proportional technical shaping artifacts; output: tech spec, ADR / decision memo, or related technical artifact; use when: technical shape needs durable documentation.
/ai-rpi-protocol/skills/write-prd.md - purpose: create proportional product shaping artifacts; output: user story, PRD, or related product framing artifact; use when: product intent needs durable clarification.
/ai-rpi-protocol/skills/automated-tests.md - purpose: generate tests matching project house style; output: test files + validation; use when: user asks to add, generate, or write tests.
/ai-rpi-protocol/skills/code-review.md - purpose: strongest multi-agent code review workflow with specialist subagents; output: aggregated findings; use when: user asks to review, audit, or examine code.

/ai-rpi-protocol/core/rules/first-interaction.md - purpose: first message behavior; output: concise restatement + optional posture + next step; use when: first user interaction only.
/ai-rpi-protocol/core/rules/input-rules.md - purpose: handle any user input safely; output: clarified intent + scoped next action; use when: every user message.
/ai-rpi-protocol/core/rules/output-rules.md - purpose: preflight for responses; output: compliant response + required headers; use when: before any user facing output.
/ai-rpi-protocol/core/rules/self-check.md - purpose: detect violations before shipping text/code; output: corrections list + fixed output; use when: before decisions or output.
/ai-rpi-protocol/core/rules/formatting-rules.md - purpose: standardize response format; output: consistent structure; use when: any user facing output.
/ai-rpi-protocol/core/rules/think-first-protocol.md - purpose: enforce challenge and trade offs; output: 1 to 3 friction points + alternatives; use when: every response.
/ai-rpi-protocol/core/rules/anti-eager-beaver.md - purpose: prevent rushing to help; output: deliberate pause + follow instructions; use when: urge to answer/act fast.
/ai-rpi-protocol/core/rules/anti-sycophancy.md - purpose: prevent yes machine behavior; output: positive friction + risks + options; use when: decisions, trade-offs, or weak requirements surface.
/ai-rpi-protocol/core/rules/topic-drift.md - purpose: prevent scope switch token burn; output: handoff suggestion + prompt; use when: user changes task mid thread.
/ai-rpi-protocol/core/rules/escape-commands.md - purpose: let user bypass governance; output: direct response mode + resume path; use when: user explicitly bypasses.
/ai-rpi-protocol/core/rules/phases.md - purpose: define RPI flow; output: phase gates + transitions; use when: starting any phase.
/ai-rpi-protocol/core/rules/memory-handling.md - purpose: memory workflow; output: what to write and when; use when: phase transitions or decision points.
/ai-rpi-protocol/core/rules/context-attention.md - purpose: apply progressive loading operationally; output: what to load, what to skip, and when to compact; use when: before loading any file.
/ai-rpi-protocol/core/rules/token-discipline.md - purpose: keep progressive loading compact; output: lean chat summaries + referenced memory artifacts; use when: every task, every phase, every response.
/ai-rpi-protocol/core/rules/code-generation-rules.md - purpose: enforce code quality after generation; output: linter check + pattern compliance; use when: after generating or modifying code.
/ai-rpi-protocol/core/rules/on-files-changed.md - purpose: trigger post-change checks whenever files get changed; output: lint run, project-info update check, repo checks; use when: after any turn where project files were created, modified, or deleted.
/ai-rpi-protocol/core/rules/compliance-checklist.md - purpose: observable protocol compliance indicators; output: green/red flags + recovery actions; use when: verifying AI is following the protocol.
/ai-rpi-protocol/core/rules/engineering-best-practices.md - purpose: enforce well-known engineering best practices; output: suggestions + flags during Planning and Implementation; use when: always loaded.
/ai-rpi-protocol/core/rules/anti-hallucination.md - purpose: prevent confident references to things that don't exist; output: verified claims + explicit uncertainty; use when: every response that references APIs, libraries, methods, or config.
/ai-rpi-protocol/core/rules/confidence-calibration.md - purpose: distinguish verified facts from guesses; output: calibrated confidence signals; use when: every response with technical claims.
/ai-rpi-protocol/core/rules/anti-anchoring.md - purpose: prevent fake options that dress up a single idea as multiple; output: genuinely distinct alternatives; use when: Planning phase, any multi-option response.
/ai-rpi-protocol/core/rules/questions-format.md - purpose: standardize how questions are asked; output: question + explanation + recommendation; use when: asking open questions, clarifying questions, or presenting choices.
/ai-rpi-protocol/core/rules/self-improvement.md - purpose: learn from mistakes across sessions; output: lessons written to memory; use when: user corrects the AI or points out a mistake.

/ai-rpi-protocol/core/phases/research.md - purpose: guide investigation; output: findings with evidence; use when: Research phase.
/ai-rpi-protocol/core/phases/planning.md - purpose: design before code; output: 2 to 3 options + trade offs; use when: Plan phase.
/ai-rpi-protocol/core/phases/planning-prd-techspec-guidance.md - purpose: shaping artifact guidance beyond the brief plan; output: when to recommend heavier shaping artifacts, where to store them, and how to keep them proportional; use when: Plan phase at lite or full.
/ai-rpi-protocol/core/phases/implementation.md - purpose: execute approved plan; output: working code + finish discipline; use when: Implement phase.

/ai-rpi-protocol/templates/project-info-generation/project-info-file-structure.md - purpose: define project info files; output: file list and one line rules; use when: generating or validating project info.
/ai-rpi-protocol/templates/project-info-generation/project-info-loading-guide.md - purpose: load project truths; output: what to load based on task; use when: before Research if project-info exists.
/ai-rpi-protocol/templates/project-info-generation/generate-project-info-mode.md - purpose: bootstrap or repair project-info; output: generate/update flow and file list; use when: project-info is missing, partial, or the user asks to generate it.
/ai-rpi-protocol/templates/project-info-generation/generate-project-info-workflow.md - purpose: bootstrap or update project-info by researching the codebase; output: stable project-info files preserved in place; use when: generating or repairing project-info.
/ai-rpi-protocol/templates/project-info-generation/memory-template.md - purpose: template for project memory; output: content to write to /ai-rpi-protocol_project-info/memory.md; use when: generating project info.
/ai-rpi-protocol/templates/project-info-generation/user-preferences-template.md - purpose: template for project user preferences; output: content to write to /ai-rpi-protocol_project-info/user-preferences.md; use when: generating project info.

/ai-rpi-protocol/templates/restate-feature-request.md - purpose: restate feature request; output: scoped spec; use when: new feature ask.
/ai-rpi-protocol/templates/restate-bugfix-request.md - purpose: restate bugfix; output: reproduction + expected behavior; use when: bug reports.
/ai-rpi-protocol/templates/restate-code-review-request.md - purpose: clarify ambiguous code review scope; output: scoped review spec; use when: the review target or comparison surface is unclear.
/ai-rpi-protocol/templates/code-review-output-template.md - purpose: code review per-issue output template; output: structured advice per issue; use when: the Code Review skill aggregates findings or Planning needs per-issue review guidance.
/ai-rpi-protocol/templates/restate-other-request.md - purpose: restate misc asks; output: clarified scope; use when: unclear task type.
/ai-rpi-protocol/templates/context-handoff-artifact.md - purpose: clean restart template; output: copyable new chat prompt; use when: topic drift or phase handoff.
/ai-rpi-protocol/templates/welcome-message.md - purpose: first message template; output: concise restatement + optional operating posture; use when: first user interaction.
/ai-rpi-protocol/templates/plan-output-template.md - purpose: plan artifact template; output: structured plan .md; use when: Planning phase output.
/ai-rpi-protocol/templates/benchmark-case-template.md - purpose: lean benchmark or golden-case template for AI-RPI evaluation; output: one representative case with outcome and protocol-quality signals; use when: capturing benchmark cases, golden cases, or lessons-worthy scenarios.
/ai-rpi-protocol/templates/prd-template-micro.md - purpose: minimal PRD for small features; output: single-page PRD; use when: Plan phase, size = micro.
/ai-rpi-protocol/templates/prd-template-condensed.md - purpose: condensed PRD; output: structured PRD; use when: Plan phase, size = condensed.
/ai-rpi-protocol/templates/prd-template-full.md - purpose: full PRD for complex features; output: comprehensive PRD; use when: Plan phase, size = full.
/ai-rpi-protocol/templates/tech-spec-template-condensed.md - purpose: condensed Tech Spec; output: structured Tech Spec; use when: Plan phase, tech-centric, size = condensed.
/ai-rpi-protocol/templates/tech-spec-template-full.md - purpose: full Tech Spec; output: comprehensive Tech Spec; use when: Plan phase, tech-centric, size = full.
/ai-rpi-protocol/templates/request-types-reference.md - purpose: classify user requests into public Modes; output: which template to use; use when: unclear request type.

/ai-rpi-protocol/artifacts/ - purpose: recommended shareable artifact root; output: shaping/ and delivery/ directories for saved artifacts; use when: storing shareable artifacts outside session memory.
/ai-rpi-protocol/artifacts/README.md - purpose: explain the recommended artifacts layout; output: artifact directory intent, naming guidance, and compatibility notes; use when: deciding where to save shaping or delivery artifacts.
/ai-rpi-protocol/artifacts/shaping/ - purpose: recommended shareable shaping artifact directory; output: user stories, PRDs, tech specs, ADRs, and related shaping docs; use when: saving shaping artifacts.
/ai-rpi-protocol/artifacts/delivery/ - purpose: recommended shareable delivery artifact directory; output: PR descriptions, review packages, handoff notes, validation summaries, diagrams, and related delivery docs; use when: saving delivery artifacts.

/ai-rpi-protocol/agents/codebase-mapper.md - purpose: map or deeply investigate the relevant codebase slice; output: evidence-backed findings, constraints, and likely blast radius; use when: repo understanding is incomplete or broad codebase research is needed.
/ai-rpi-protocol/agents/challenger.md - purpose: apply positive friction across phases; output: challenged assumptions, trade-offs, and stronger alternatives; use when: the work needs an independent critical pass.
/ai-rpi-protocol/agents/code-reviewer.md - purpose: review correctness, maintainability, clarity, and reviewer readiness; output: prioritized review findings; use when: a code review lens is needed.
/ai-rpi-protocol/agents/debugger.md - purpose: isolate likely root causes and failure paths; output: evidence-backed diagnostic findings; use when: the bug is not yet well understood.
/ai-rpi-protocol/agents/performance-reviewer.md - purpose: review efficiency, scale behavior, and bottlenecks; output: performance risks and guidance; use when: performance could materially change.
/ai-rpi-protocol/agents/documentation-researcher.md - purpose: find current external documentation or references; output: confirmed external facts and caveats; use when: repo evidence is insufficient.
/ai-rpi-protocol/agents/packaging-reviewer.md - purpose: improve reviewability and handoff quality; output: stronger PR or handoff packaging; use when: the result needs cleaner review framing.
/ai-rpi-protocol/agents/web-researcher.md - purpose: web search when codebase insufficient; output: docs, APIs, best practices; use when: answer not in codebase.
/ai-rpi-protocol/agents/code-review/security-reviewer.md - purpose: security-focused code review subagent; output: security findings; use when: Code Review skill Phase 3.
/ai-rpi-protocol/agents/standards-discovery.md - purpose: discover project conventions; output: discovered standards artifact; use when: Code Review, project-info generation, Planning, or any task needing project context.
/ai-rpi-protocol/agents/code-review/conventions-reviewer.md - purpose: conventions code review using discovered standards; output: convention violations; use when: Code Review skill Phase 4.
/ai-rpi-protocol/agents/code-review/architecture-reviewer.md - purpose: architecture-focused code review subagent; output: design findings; use when: Code Review skill Phase 3.
/ai-rpi-protocol/agents/code-review/test-quality-reviewer.md - purpose: test quality code review subagent; output: test validity findings; use when: Code Review skill Phase 3.
/ai-rpi-protocol/agents/code-review/patterns-reviewer.md - purpose: patterns and naming code review subagent; output: consistency findings; use when: Code Review skill Phase 3.
/ai-rpi-protocol/agents/code-review/documentation-reviewer.md - purpose: documentation-focused code review subagent; output: docs sync findings; use when: Code Review skill Phase 3.

/ai-rpi-protocol/adapters/README.md - purpose: explain adapters; output: where to find IDE/model specifics; use when: setup or troubleshooting.
/ai-rpi-protocol/adapters/ides/cursor.md - purpose: Cursor rules and feature leverage; output: mandatory rules + features; use when: running in Cursor.
/ai-rpi-protocol/adapters/ides/claude-code.md - purpose: Claude Code rules and feature leverage; output: mandatory rules + features; use when: running in Claude Code.
/ai-rpi-protocol/adapters/ides/codex.md - purpose: Codex rules and feature leverage; output: mandatory rules + features; use when: running in Codex.
/ai-rpi-protocol/adapters/ides/vscode.md - purpose: VS Code Copilot rules and feature leverage; output: mandatory rules + features; use when: running in VS Code Copilot.
/ai-rpi-protocol/adapters/ides/zed.md - purpose: Zed rules and feature leverage; output: mandatory rules + features; use when: running in Zed.
/ai-rpi-protocol/adapters/ides/windsurf.md - purpose: Windsurf rules and feature leverage; output: mandatory rules + features; use when: running in Windsurf.
/ai-rpi-protocol/adapters/models/claude.md - purpose: Claude/Anthropic model behavior notes; output: compliance tweaks; use when: running Claude or Anthropic models.
/ai-rpi-protocol/adapters/models/gpt.md - purpose: GPT model behavior notes; output: compliance tweaks; use when: running GPT models.
/ai-rpi-protocol/adapters/models/deepseek.md - purpose: DeepSeek model behavior notes; output: compliance tweaks; use when: running DeepSeek models.
/ai-rpi-protocol/adapters/models/gemini.md - purpose: Gemini model behavior notes; output: compliance tweaks; use when: running Gemini models.
/ai-rpi-protocol/adapters/models/grok.md - purpose: Grok model behavior notes; output: compliance tweaks; use when: running Grok models.
/ai-rpi-protocol/adapters/models/local.md - purpose: local model behavior notes; output: compliance tweaks; use when: running local/small models.

/ai-rpi-protocol/docs/01-ai-sycophancy-the-yes-machine-problem.md - purpose: explain the yes-machine failure mode in AI coding; output: positioning-ready argument for anti-sycophancy; use when: writing, teaching, or justifying positive friction.
/ai-rpi-protocol/docs/02-the-eager-beaver-problem.md - purpose: explain why premature execution harms engineering outcomes; output: framing for deliberate pacing and better task shaping; use when: explaining anti-rush discipline.
/ai-rpi-protocol/docs/03-hallucination-is-not-a-bug.md - purpose: explain hallucination as a systems problem, not just a model flaw; output: framing for verification-first workflows; use when: teaching anti-hallucination discipline.
/ai-rpi-protocol/docs/04-anchoring-bias-three-options-really-one.md - purpose: explain fake-option planning drift; output: framing for genuinely distinct alternatives; use when: justifying anti-anchoring rules.
/ai-rpi-protocol/docs/05-what-mcp-servers-actually-change.md - purpose: explain how tool access changes agent capability and risk; output: framing for harness and operating-rule design; use when: discussing MCP and agent tooling.
/ai-rpi-protocol/docs/06-context-windows-the-invisible-constraint.md - purpose: explain context limits as an engineering constraint; output: framing for progressive loading and memory discipline; use when: discussing context management.
/ai-rpi-protocol/docs/07-gates-why-friction-makes-you-faster.md - purpose: explain why deliberate gates improve throughput; output: positioning for proportional governance; use when: defending RPI gates or friction.
/ai-rpi-protocol/docs/08-vibe-coding-vs-evidence-based-coding.md - purpose: contrast improvisational AI use with evidence-based engineering; output: positioning for validation and review discipline; use when: explaining AI-RPI's engineering stance.
/ai-rpi-protocol/docs/09-ai-as-exoskeleton-not-replacement.md - purpose: explain the engineer-in-control posture; output: framing for augmentation over autonomy; use when: positioning AI-RPI's human-control model.
/ai-rpi-protocol/docs/10-consistency-over-heroics.md - purpose: explain why repeatable systems beat occasional AI wins; output: framing for process reliability over demos; use when: discussing sustainable agent workflows.
/ai-rpi-protocol/docs/11-harness-engineering-and-the-missing-half.md - purpose: explain why output quality needs decision-quality support too; output: framing for challenge, shaping, and governance; use when: discussing harness engineering.
/ai-rpi-protocol/docs/12-are-you-still-using-prompts.md - purpose: position protocols against prompt-only workflows; output: messaging for AI-RPI as a system, not a prompt pack; use when: explaining differentiation.
/ai-rpi-protocol/docs/13-stop-prompting-like-a-chatbot.md - purpose: explain why software work needs stronger operating structure than ad hoc prompting; output: framing for repo-native protocol use; use when: explaining practical agent workflows.
/ai-rpi-protocol/docs/14-protocols-will-replace-prompts.md - purpose: argue for protocols as the durable coordination surface; output: high-level positioning for AI-RPI; use when: writing or comparing workflow approaches.
/ai-rpi-protocol/docs/16-the-future-developer-workflow.md - purpose: explore how coding work changes under agentic tooling; output: forward-looking positioning and workflow framing; use when: discussing AI-native engineering practice.
/ai-rpi-protocol/docs/claude-code-skills-integration.md - purpose: explain how Claude Code Skills relate to AI-RPI's canonical contract; output: integration guidance and boundaries; use when: aligning skills with adapters and protocol semantics.
/ai-rpi-protocol/docs/launch-kit.md - purpose: package positioning and launch assets for AI-RPI; output: messaging, rollout ideas, and promotional material; use when: launch planning or product communication.
/ai-rpi-protocol/docs/rpi-protocol-vs-developer-diamond.md - purpose: compare AI-RPI with the Developer Diamond; output: differentiation points and nuanced trade-offs; use when: explaining product positioning or competitive framing.

/ai-rpi-protocol_project-info/overview.md - purpose: project identity and capabilities; output: what to load for context; use when: Research or onboarding.
/ai-rpi-protocol_project-info/constraints.md - purpose: non-negotiable rules and limits; output: what to respect in plans/code; use when: Research and Planning.
/ai-rpi-protocol_project-info/structure.md - purpose: repo layout and areas; output: where to find files; use when: navigating codebase.
/ai-rpi-protocol_project-info/glossary.md - purpose: domain terms; output: definitions for context; use when: encountering domain terms.
/ai-rpi-protocol_project-info/standards.md - purpose: coding and formatting standards; output: what to follow in code; use when: Implementation or review.
/ai-rpi-protocol_project-info/stack-patterns.md - purpose: stack and pattern conventions; output: how to structure code; use when: Planning and Implementation.
/ai-rpi-protocol_project-info/integrations.md - purpose: external systems and APIs; output: integration context; use when: research involves external services.
/ai-rpi-protocol_project-info/monitoring.md - purpose: logging, metrics, observability; output: monitoring context; use when: research involves logging or metrics.
/ai-rpi-protocol_project-info/memory.md - purpose: durable project memory; output: stable project-specific facts, pitfalls, and workflow knowledge to remember across sessions and upgrades; use when: always load early if present.
/ai-rpi-protocol_project-info/user-preferences.md - purpose: durable project-scoped user preferences; output: stable ways of working to honor early on every interaction; use when: always load early if present.

/ai-rpi-protocol/plans/ - purpose: legacy plan-only compatibility directory; output: older PRD and Tech Spec deliverables; use when: a repo still uses plans/ instead of artifacts/shaping/.
/ai-rpi-protocol/plans/README.md - purpose: explain when to keep using the legacy plans directory; output: compatibility guidance and fallback storage notes; use when: deciding between plans/ and artifacts/.
/ai-rpi-protocol/memory/session-state.md - purpose: current task and phase status; output: session state artifact; use when: phase transitions or resume.
/ai-rpi-protocol/memory/research-cache.md - purpose: research findings with evidence; output: research cache artifact; use when: Research completed.
/ai-rpi-protocol/memory/decisions.md - purpose: decisions and rationale; output: decisions artifact; use when: meaningful decision or trade off.
/ai-rpi-protocol/memory/metrics-log.md - purpose: lightweight task-quality and protocol-quality log; output: lean metrics rows; use when: Implementation completed or "show metrics" command.
/ai-rpi-protocol/memory/lessons.md - purpose: mistake patterns and prevention guidance captured across sessions; output: lessons to re-apply after corrections or failures; use when: reviewing durable behavioral improvements.
