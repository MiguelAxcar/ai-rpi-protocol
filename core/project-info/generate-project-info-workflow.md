purpose: generate project-info by researching codebase; output: stable project-info files; use when: Generate Project Info mode.

# Generate Project Info

## Purpose

Generate project-specific files by researching codebase deeply and asking user for missing info.

**CRITICAL:** This mode BLOCKS all RPI Protocol phases. Do NOT proceed to R >> P >> I until all files are generated OR user explicitly ignores.

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

**Do this FIRST using `/ai-rpi-protocol/agents/codebase-researcher.md`:**

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

**Use:** Semantic search, grep, file reading, codebase-researcher agent

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

MANDATORY: it should only start generating when user tells that there aren't anything else to share related to project context.


### Step 3: Interact with user to generate each file

**CRITICAL:** Be thoughtful ans ask questions when you want to confirm anything. Ask questions easier to be answered, example, option A, B, C. Only ask for clarifications if you are trully unsure. Avoid to document on project info data that will potentially change in the near future, try to capture the real truths from the project which won't change within time.

**Generate these files:**

#### File 1: `overview.md`
**Capture:** Fundamental identity that won't change
- What this project IS (domain, business purpose) - stable
- Who uses it (user TYPES, roles) - stable
- Core capabilities (what it DOES, not current feature list) - stable
- Tech stack (languages, frameworks, databases) - stable
- Deployment model (cloud, on-prem, hybrid) - stable

**Avoid:** Feature roadmaps, team structure, version numbers, "we're building X"

#### File 2: `constraints.md`
**Capture:** Non-negotiable rules that define boundaries
- Compliance requirements (HIPAA, PCI, GDPR, SOC2) - stable (regulatory)
- Security rules (auth patterns, data protection) - stable
- Performance SLAs (if contractual) - stable
- Database rules (hot tables, migration patterns) - stable
- Data handling rules (PHI, PII, client data, sensitive data) - stable

**Avoid:** Current performance numbers, temporary restrictions, "until we migrate"

#### File 3: `structure.md`
**Capture:** Architectural decisions that define organization
- Project structure (monorepo, microservices, single app) - stable
- Key directory PURPOSES (not exhaustive listing) - stable
- Architectural patterns (MVC, service layer, clean architecture) - stable
- Module organization PHILOSOPHY - stable

**Avoid:** Listing every directory/file, current file counts, "we're adding X module"

#### File 4: `stack-patterns.md`
**Capture:** Established patterns that define "how we code here"
- Framework patterns (NestJS modules, React hooks, etc.) - stable
- File naming conventions - stable
- Code organization patterns - stable
- Design patterns used (repository, factory, etc.) - stable
- Error handling patterns - stable
- Testing patterns - stable

**Avoid:** Patterns under debate, experimental approaches, "we're trying X"

#### File 5: `glossary.md`
**Capture:** Domain language that defines shared understanding
- Business domain terms (core concepts) - stable
- Technical terms specific to this project - stable
- Acronyms and abbreviations - stable
- Entity/domain model terms (core entities) - stable

**Avoid:** Feature names that may be renamed, temporary codenames, internal jokes

#### File 6: `standards.md`
**Capture:** Enforced rules that define quality expectations
- Code formatting rules (tools and configs used) - stable
- Type safety rules (no `any`, strict mode, etc.) - stable
- Testing standards (required test types, coverage thresholds) - stable
- Git practices (branch naming, commit format) - stable
- Code review requirements - stable

**Avoid:** Current coverage percentages, specific tool versions, "we plan to add X"

**Optional files (only if detected):**

#### File 7: `integrations.md` (If external integrations exist)
**Capture:** Integration patterns and requirements
- External services we DEPEND on (not might use someday) - stable
- Authentication PATTERNS (OAuth, API keys) - stable
- Error handling patterns - stable
- Webhook patterns - stable

**Avoid:** Specific API versions, rate limit numbers (change), "we're evaluating X"

#### File 8: `monitoring.md` (If production monitoring exists)
**Capture:** Observability patterns and requirements
- Logging strategy (structured logs, required fields) - stable
- Monitoring tools we USE (not evaluating) - stable
- Tracing patterns (trace ID propagation) - stable
- Error tracking requirements - stable

**Avoid:** Alert thresholds (tuned frequently), dashboard names, "we're adding X"

### Rules

- **Stability first:** Only document what won't change soon. Ask if uncertain.
- **Deep research first:** Use codebase-researcher agent, don't guess
- **Ask critical questions:** Get user input before generating
- **Ephemeral detection:** If something seems temporary, ASK before including
- **Stack detection:** Detect actual stack from codebase, adapt patterns accordingly
- **Optional files:** Only generate if detected in research, skip if not applicable
- Save all files to `/ai-rpi-protocol_project-info/`

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

### Step 5: ASK USER CONFIRMATION

Heading: 🔔 REVIEW & APPROVE

Ask user to go to the target directory, file by file, edit and review it. Or ask for changes.

Interact with user applying AI RPI Framework concepts until all editions is done, and the user is COMPLETELY owner of the generated files.

Be thoughtful here.

### Step 6: Finish generation

- Display success message
- Show that AI RPI Framework is ready to proceed with user task
- Ask user confirmation
- Exit Generate Project Info Mode
- Proceed to RPI Protocol initialization showing encouraging message

**Exit Generate Project Info Mode, continue to RPI Protocol initialization.**


