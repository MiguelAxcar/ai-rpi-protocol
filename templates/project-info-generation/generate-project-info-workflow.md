purpose: bootstrap or update project-info by researching codebase; output: stable project-info files preserved in place; use when: generating or repairing project-info.

# Generate Project Info

## Purpose

Bootstrap or repair project-specific files by researching the codebase deeply and asking the user for missing info.

**Setup lifecycle rule:** Project-info improves future work, but it is not a hard blocker. If the user wants to defer it, proceed with the task and treat project-info as follow-up bootstrap or repair work.

**Durability rule:** Generate project-info once, then update it in place. Do not recreate durable files from scratch unless the user explicitly wants a reset.

---

## Stability Principle (CRITICAL)

**Project-info captures STABLE, ALWAYS-TRUE information - not ephemeral details.**

### What to Document (Stable)

| Category | Examples |
|----------|----------|
| **Core Identity** | What the project IS, its domain, business purpose |
| **Fundamental Constraints** | Compliance (HIPAA, PCI), security requirements |
| **Architecture** | Monorepo vs microservices, core patterns |
| **Stack** | Languages, frameworks, databases (unlikely to change) |
| **Domain Terms** | Business glossary, entity names |
| **Coding Standards** | Linting rules, naming conventions |

### What NOT to Document (Ephemeral)

| Category | Examples | Why Ephemeral |
|----------|----------|---------------|
| **Current State** | "We're migrating from X to Y" | Will change |
| **Version Numbers** | "Using React 18.2.0" | Changes frequently |
| **Team Structure** | "John owns the payments module" | People change |
| **Active Features** | "We're building feature X" | Will be done |
| **Temporary Workarounds** | "Due to bug in X, we do Y" | Will be fixed |
| **Counts/Numbers** | "We have 50 API endpoints" | Changes constantly |

### When Uncertain - ASK

If you detect something that MIGHT be ephemeral:

```
⚠️ This seems potentially ephemeral:
   "[detected information]"

Options:
A) Include it (it's stable, won't change soon)
B) Skip it (it's temporary/changing)
C) Rephrase as: "[suggested stable version]"

Your choice?
```

**Examples:**
- ❌ "We use Redis 7.2" >> ⚠️ Version may change
- ✅ "We use Redis for caching and session storage" >> Stable purpose
- ❌ "The team is refactoring the auth module" >> ⚠️ Temporary state
- ✅ "Auth uses JWT tokens with refresh rotation" >> Stable pattern

---

## MANDATORY: Follow This Process Exactly

### Step 1: Deep Codebase Research

**Do this FIRST using `/ai-rpi-protocol/agents/codebase-mapper.md` (Depth: `deep`):**

1. **Locate** >> Find key files, structure, entry points
2. **Analyze** >> Understand how code works, patterns, architecture
3. **Pattern Match** >> Find similar examples, conventions

**Research areas:**
- Project structure (monorepo, microservices, single app, etc.)
- Stack detection (package.json, composer.json, requirements.txt, Cargo.toml, pom.xml, etc.)
- Framework identification (NestJS, Express, Django, Rails, React, Vue, etc.)
- Language detection (TypeScript, Python, Java, Go, Rust, etc.)
- Domain patterns (entities, workflows, key features)
- Constraints detection (compliance, security, performance requirements)
- Integration detection (API clients, webhooks, external services)
- Observability detection (logging libraries, metrics, monitoring tools)
- Existing documentation or comments

**Use:** Semantic search, grep, file reading, codebase-mapper subagent

### Step 2: Ask Critical Questions

**Before generating files, ask user for critical information:**

```
📋 Quick Questions (helps me generate better files):

1️⃣ Compliance: Any requirements? (HIPAA, PCI, GDPR, SOC2, none)
2️⃣ Hot Tables: Any entities/tables that need careful migrations?
3️⃣ Security: Any critical security requirements or constraints?
4️⃣ Glossary: Any domain terms I should know?

Show a very highlighted message asking user to share any sort of doc it may have about project, technical descriptions, PDF, images, READMEs, links, etc.

💬 Your answers (can skip if unsure):
```

IMPORTANT: Feel free to ASK anything you may find useful, such as contract of API, description of product X, how X connects to Y, why this is used for, etc and use it as context, writing where needed.

MANDATORY: it should only start generating or repairing when user tells that there aren't anything else to share related to project context.


### Step 3: Interact with user to generate each file

**CRITICAL:** Be thoughtful and ask questions when you want to confirm anything. Ask questions that are easy to answer, for example option A, B, or C. Only ask for clarifications if you are truly unsure. Avoid documenting project-info data that will potentially change in the near future; try to capture the real truths from the project that will not change with time.

Before writing files, decide whether this is:
- **bootstrap**: files are missing and need first-time creation
- **repair**: files exist and need targeted updates in place

Repair rules:
- preserve user-written durable context unless it is clearly wrong or the user wants it changed
- update existing files in place instead of replacing the whole directory
- never silently erase `memory.md` or `user-preferences.md`
- if a required file is missing, create only the missing file unless a broader repair is clearly needed
- if `memory.md` is missing, create it immediately instead of waiting for a full regeneration pass

**Generate these files:**

#### File 1: `memory.md`
**Capture:** Durable project memory that should survive sessions and upgrades
- Stable project-specific facts worth remembering
- Repeated pitfalls and prevention rules
- Durable workflow knowledge that reduces repetition
- Important lessons that should remain attached to the project

**Avoid:** One-off task notes, temporary migrations, volatile implementation status

#### File 2: `user-preferences.md`
**Capture:** Stable user preferences for this project
- Confirmed project-scoped preferences
- Preferred validation or handoff behavior
- Stable repo-specific workflow choices
- Inferred likely preferences only when clearly labeled and worth preserving

**Avoid:** Temporary task requests, weak guesses, one-time instructions

#### File 3: `overview.md`
**Capture:** Fundamental identity that won't change
- What this project IS (domain, business purpose) - stable
- Who uses it (user TYPES, roles) - stable
- Core capabilities (what it DOES, not current feature list) - stable
- Tech stack (languages, frameworks, databases) - stable
- Deployment model (cloud, on-prem, hybrid) - stable

**Avoid:** Feature roadmaps, team structure, version numbers, "we're building X"

#### File 4: `constraints.md`
**Capture:** Non-negotiable rules that define boundaries
- Compliance requirements (HIPAA, PCI, GDPR, SOC2) - stable (regulatory)
- Security rules (auth patterns, data protection) - stable
- Performance SLAs (if contractual) - stable
- Database rules (hot tables, migration patterns) - stable
- Data handling rules (PHI, PII, client data, sensitive data) - stable

**Avoid:** Current performance numbers, temporary restrictions, "until we migrate"

#### File 5: `structure.md`
**Capture:** Architectural decisions that define organization
- Project structure (monorepo, microservices, single app) - stable
- Key directory PURPOSES (not exhaustive listing) - stable
- Architectural patterns (MVC, service layer, clean architecture) - stable
- Module organization PHILOSOPHY - stable

**Avoid:** Listing every directory/file, current file counts, "we're adding X module"

#### File 6: `stack-patterns.md`
**Capture:** Established patterns that define "how we code here"
- Framework patterns (NestJS modules, React hooks, etc.) - stable
- File naming conventions - stable
- Code organization patterns - stable
- Design patterns used (repository, factory, etc.) - stable
- Error handling patterns - stable
- Testing patterns - stable

**Avoid:** Patterns under debate, experimental approaches, "we're trying X"

#### File 7: `glossary.md`
**Capture:** Domain language that defines shared understanding
- Business domain terms (core concepts) - stable
- Technical terms specific to this project - stable
- Acronyms and abbreviations - stable
- Entity/domain model terms (core entities) - stable

**Avoid:** Feature names that may be renamed, temporary codenames, internal jokes

#### File 8: `standards.md`
**Capture:** Enforced rules that define quality expectations
- Code formatting rules (tools and configs used) - stable
- Type safety rules (no `any`, strict mode, etc.) - stable
- Testing standards (required test types, coverage thresholds) - stable
- Git practices (branch naming, commit format) - stable
- Code review requirements - stable

**Avoid:** Current coverage percentages, specific tool versions, "we plan to add X"

**Optional files (only if detected):**

#### File 9: `integrations.md` (If external integrations exist)
**Capture:** Integration patterns and requirements
- External services we DEPEND on (not might use someday) - stable
- Authentication PATTERNS (OAuth, API keys) - stable
- Error handling patterns - stable
- Webhook patterns - stable

**Avoid:** Specific API versions, rate limit numbers (change), "we're evaluating X"

#### File 10: `monitoring.md` (If production monitoring exists)
**Capture:** Observability patterns and requirements
- Logging strategy (structured logs, required fields) - stable
- Monitoring tools we USE (not evaluating) - stable
- Tracing patterns (trace ID propagation) - stable
- Error tracking requirements - stable

**Avoid:** Alert thresholds (tuned frequently), dashboard names, "we're adding X"

### Rules

- **Stability first:** Only document what won't change soon. Ask if uncertain.
- **Deep research first:** Use codebase-mapper subagent in `deep` mode, don't guess
- **Ask critical questions:** Get user input before generating
- **Ephemeral detection:** If something seems temporary, ASK before including
- **Stack detection:** Detect actual stack from codebase, adapt patterns accordingly
- **Optional files:** Only generate if detected in research, skip if not applicable
- Save all files to `/ai-rpi-protocol_project-info/`, including `memory.md` and `user-preferences.md`.
- Prefer updating files in place over full regeneration.

### Ephemeral Detection Triggers

Ask user confirmation if you detect:
- Version numbers (specific versions like "18.2.0")
- Counts ("50 endpoints", "12 services")
- Temporal language ("currently", "for now", "until we", "migrating to")
- Names of people or teams
- Active work ("building", "refactoring", "planning")
- Dates or deadlines
- Workarounds or temporary solutions

### Step 4: WHEN ALL FILES WERE GENERATED
- Show names and contents of generated files

### Step 4b: PROMPT USER TO REVIEW DURABLE PREFERENCES

**Explicitly tell the user:** After project info files are loaded, **review `user-preferences.md` and edit it** with your durable project-scoped preferences. The assistant will load this file early on every interaction, so anything you add here applies across Research, Planning, and Implementation.

**Give the user examples of what they can add**, such as:
- "When commenting code, explain **why** something is done, not **what** it does."
- "Prefer descriptive variable names over short ones; avoid single-letter names except loop counters."
- "When suggesting refactors, always preserve or add tests first."
- "Mention breaking changes explicitly in commit messages and PR descriptions."
- "Use plain language for trade-offs; avoid jargon unless the domain requires it."

Then continue to Step 5.

### Step 5: ASK USER CONFIRMATION

Heading: 🔔 REVIEW & APPROVE

Ask user to go to the target directory, file by file, edit and review it. Or ask for changes.

Interact with user applying AI RPI Protocol concepts until all editions is done, and the user is COMPLETELY owner of the generated files.

Be thoughtful here.

### Step 6: Finish generation

- Display success message
- Show whether bootstrap or repair completed
- Show that AI RPI Protocol is ready to proceed with user task
- Ask user confirmation
- Exit Generate Project Info Mode
- Proceed to RPI Protocol initialization or return to the deferred task

**Exit Generate Project Info Mode, continue to RPI Protocol initialization.**
