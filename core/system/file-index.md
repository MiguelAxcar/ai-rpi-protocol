purpose: file map and load order; output: list of path + purpose/output/use when; use when: always first or before loading any file.

/ai-rpi-protocol/core/system/protocol-full.md - purpose: enforce protocol and load order (full mode); output: hard blockers + references; use when: mode is set to full.
/ai-rpi-protocol/core/system/protocol-lite.md - purpose: lean protocol entry point (lite mode); output: core files + on-demand loading; use when: mode is set to lite or not set.
/ai-rpi-protocol/AGENTS.md - purpose: entry point; ask user, detect mode, route to protocol-lite or protocol-full; output: protocol loading; use when: every new conversation.
/ai-rpi-protocol/CLAUDE.md - purpose: Claude Code entry point; output: loads AGENTS.md; use when: Claude Code CLI or VS Code extension.
/ai-rpi-protocol/README.md - purpose: project intro and setup; output: what RPI is and how to install; use when: onboarding or reference.
/ai-rpi-protocol/CHANGELOG.md - purpose: version history; output: notable changes; use when: checking releases or version.
/ai-rpi-protocol/CONTRIBUTING.md - purpose: how to contribute; output: contribution guidelines; use when: contributing or PRs.
/ai-rpi-protocol/WISHLIST.md - purpose: future improvements; output: wishlist items; use when: planning features or roadmap.
/ai-rpi-protocol/METRICS.md - purpose: how to measure protocol effectiveness; output: what to track and when to adjust; use when: evaluating protocol value.

/ai-rpi-protocol/core/system/file-index.md - purpose: file map and load order; output: list of path + purpose/output/use when; use when: always first or before loading any file.
/ai-rpi-protocol/core/system/modes.md - purpose: define mode selection; output: mode choice (Quick/Thoughtful/Comprehensive); use when: start of request or re-assess.
/ai-rpi-protocol/core/system/profiles.md - purpose: define profiles and selection rules; output: profile choice and style; use when: start of request or re-assess.
/ai-rpi-protocol/core/system/subagent-system.md - purpose: define subagent invocation; output: when and how to call subagents; use when: Research or task needs delegation.

/ai-rpi-protocol/core/rules/first-interaction.md - purpose: first message behavior; output: welcome + state + next step; use when: first user interaction only.
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
/ai-rpi-protocol/core/rules/context-attention.md - purpose: reduce token burn; output: what to load and skip; use when: before loading any file.
/ai-rpi-protocol/core/rules/token-discipline.md - purpose: reduce token burn without reducing correctness; output: lean chat summaries + referenced memory artifacts; use when: every task, every phase, every response.
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
/ai-rpi-protocol/core/phases/implementation.md - purpose: execute approved plan; output: working code + finish discipline; use when: Implement phase.

/ai-rpi-protocol/core/project-info/project-info-file-structure.md - purpose: define project info files; output: file list and one line rules; use when: generating or validating project info.
/ai-rpi-protocol/core/project-info/project-info-loading-guide.md - purpose: load project truths; output: what to load based on task; use when: before Research if project-info exists.
/ai-rpi-protocol/core/project-info/generate-project-info-mode.md - purpose: block RPI until project-info exists; output: generate flow and file list; use when: project-info empty and user accepts.
/ai-rpi-protocol/core/project-info/generate-project-info-workflow.md - purpose: generate project-info by researching codebase; output: stable project-info files; use when: Generate Project Info mode.
/ai-rpi-protocol/core/project-info/custom-instructions-template.md - purpose: template for custom-instructions.md; output: content to write to ai-rpi-protocol_project-info/custom-instructions.md; use when: generating project info.

/ai-rpi-protocol/user-preferences/preferences.md - purpose: user style and global rules; output: overrides for other rules; use when: always check early and honor precedence.

/ai-rpi-protocol/templates/restate-feature-request.md - purpose: restate feature request; output: scoped spec; use when: new feature ask.
/ai-rpi-protocol/templates/restate-bugfix-request.md - purpose: restate bugfix; output: reproduction + expected behavior; use when: bug reports.
/ai-rpi-protocol/templates/restate-code-review-request.md - purpose: restate code review request; output: scoped review spec; use when: user asks to review, audit, or examine code.
/ai-rpi-protocol/templates/code-review-output-template.md - purpose: code review per-issue output template; output: structured advice per issue; use when: Planning phase of a code review task.
/ai-rpi-protocol/templates/restate-other-request.md - purpose: restate misc asks; output: clarified scope; use when: unclear task type.
/ai-rpi-protocol/templates/context-handoff-artifact.md - purpose: clean restart template; output: copyable new chat prompt; use when: topic drift or phase handoff.
/ai-rpi-protocol/templates/welcome-message.md - purpose: first message template; output: welcome + phase + mode + profile; use when: first user interaction.
/ai-rpi-protocol/templates/plan-output-template.md - purpose: plan artifact template; output: structured plan .md; use when: Planning phase output.
/ai-rpi-protocol/templates/request-types-reference.md - purpose: classify user requests; output: which template to use; use when: unclear request type.

/ai-rpi-protocol/agents/codebase-researcher.md - purpose: deep codebase investigation subagent; output: findings with evidence; use when: Phase R needs codebase research.
/ai-rpi-protocol/agents/web-researcher.md - purpose: web search when codebase insufficient; output: docs, APIs, best practices; use when: answer not in codebase.

/ai-rpi-protocol/adapters/README.md - purpose: explain adapters; output: where to find IDE/model specifics; use when: setup or troubleshooting.
/ai-rpi-protocol/adapters/ides/cursor.md - purpose: Cursor rules and feature leverage; output: mandatory rules + features; use when: running in Cursor.
/ai-rpi-protocol/adapters/ides/claude-code.md - purpose: Claude Code rules and feature leverage; output: mandatory rules + features; use when: running in Claude Code.
/ai-rpi-protocol/adapters/ides/vscode.md - purpose: VS Code Copilot rules and feature leverage; output: mandatory rules + features; use when: running in VS Code Copilot.
/ai-rpi-protocol/adapters/ides/zed.md - purpose: Zed rules and feature leverage; output: mandatory rules + features; use when: running in Zed.
/ai-rpi-protocol/adapters/ides/windsurf.md - purpose: Windsurf rules and feature leverage; output: mandatory rules + features; use when: running in Windsurf.
/ai-rpi-protocol/adapters/models/claude.md - purpose: Claude/Anthropic model behavior notes; output: compliance tweaks; use when: running Claude or Anthropic models.
/ai-rpi-protocol/adapters/models/gpt.md - purpose: GPT model behavior notes; output: compliance tweaks; use when: running GPT models.
/ai-rpi-protocol/adapters/models/deepseek.md - purpose: DeepSeek model behavior notes; output: compliance tweaks; use when: running DeepSeek models.
/ai-rpi-protocol/adapters/models/gemini.md - purpose: Gemini model behavior notes; output: compliance tweaks; use when: running Gemini models.
/ai-rpi-protocol/adapters/models/grok.md - purpose: Grok model behavior notes; output: compliance tweaks; use when: running Grok models.
/ai-rpi-protocol/adapters/models/local.md - purpose: local model behavior notes; output: compliance tweaks; use when: running local/small models.

/ai-rpi-protocol_project-info/overview.md - purpose: project identity and capabilities; output: what to load for context; use when: Research or onboarding.
/ai-rpi-protocol_project-info/constraints.md - purpose: non-negotiable rules and limits; output: what to respect in plans/code; use when: Research and Planning.
/ai-rpi-protocol_project-info/structure.md - purpose: repo layout and areas; output: where to find files; use when: navigating codebase.
/ai-rpi-protocol_project-info/glossary.md - purpose: domain terms; output: definitions for context; use when: encountering domain terms.
/ai-rpi-protocol_project-info/standards.md - purpose: coding and formatting standards; output: what to follow in code; use when: Implementation or review.
/ai-rpi-protocol_project-info/stack-patterns.md - purpose: stack and pattern conventions; output: how to structure code; use when: Planning and Implementation.
/ai-rpi-protocol_project-info/integrations.md - purpose: external systems and APIs; output: integration context; use when: research involves external services.
/ai-rpi-protocol_project-info/monitoring.md - purpose: logging, metrics, observability; output: monitoring context; use when: research involves logging or metrics.
/ai-rpi-protocol_project-info/custom-instructions.md - purpose: user preferences and custom instructions; output: overrides and preferences to honor; use when: project info is loaded (all phases).

/ai-rpi-protocol/memory/session-state.md - purpose: current task and phase status; output: session state artifact; use when: phase transitions or resume.
/ai-rpi-protocol/memory/research-cache.md - purpose: research findings with evidence; output: research cache artifact; use when: Research completed.
/ai-rpi-protocol/memory/decisions.md - purpose: decisions and rationale; output: decisions artifact; use when: meaningful decision or trade off.
/ai-rpi-protocol/memory/metrics-log.md - purpose: task metrics log (tokens, catches, rework); output: metrics rows; use when: Implementation completed or "show metrics" command.
/ai-rpi-protocol/memory/lessons.md - purpose: mistake patterns and prevention rules; output: lessons to review at session start; use when: after user corrections.
