purpose: define project info files; output: file list and one line rules; use when: generating or validating project info.

# Project Info File Structure

## Core Principle: Stability

**Project-info captures ALWAYS-TRUE information - not ephemeral details.**

| Document | Don't Document |
|----------|----------------|
| What the project IS | What the project is BECOMING |
| Established patterns | Patterns under consideration |
| Compliance requirements | Current compliance status |
| Architecture decisions | Migration plans |
| Domain terminology | Feature codenames |
| Coding standards | Current metrics |

**Rule:** If it might change in 6 months, ask before documenting.

---

## 📋 Recommended File Set

Based on best practices and your existing codebase, here's the proposed structure:

---

## Core Files (Always Generated)

### 1. `overview.md`
**Purpose:** High-level project overview, domain, purpose, stakeholders
**Content:**
- What this project is (domain, business purpose)
- Who uses it (users, roles)
- Main features/capabilities
- Tech stack overview (languages, frameworks, databases)
- Key integrations (external services, APIs)
- Deployment environment

**Why:** Essential context for understanding project scope and purpose

---

### 2. `constraints.md`
**Purpose:** Non-negotiable rules that must never be violated
**Content:**
- Compliance requirements (HIPAA, PCI, GDPR, SOC2, etc.)
- Security rules (authentication, authorization, data protection)
- Performance constraints (SLAs, latency requirements)
- Database rules (hot tables, migration constraints, schema rules)
- Operational constraints (deployment windows, downtime tolerance)
- Data handling rules (PHI, PII, financial data, client sensitive data)

**Why:** Prevents violations that could cause outages, breaches, or compliance issues

---

### 3. `glossary.md`
**Purpose:** Domain terminology and key terms
**Content:**
- Business domain terms
- Technical terms specific to this project
- Acronyms and abbreviations
- Integration/service names
- Entity/domain model terms

**Why:** Ensures consistent language understanding across AI interactions

---

### 4. `structure.md`
**Purpose:** High-level codebase structure and organization
**Content:**
- Project structure (monorepo, microservices, single app, etc.)
- Key directories and their purposes
- Entry points (main files, API routes, frontend routes)
- Key architectural patterns (MVC, service layer, microservices, etc.)
- Module/package organization
- Build/deployment structure

**Why:** Helps AI navigate codebase efficiently, understand organization

---

### 5. `stack-patterns.md` (Stack-Specific)
**Purpose:** Coding patterns, conventions, architecture patterns for detected stack
**Content:**
- **Detected from codebase:** Framework-specific patterns
- File naming conventions
- Code organization patterns
- Architecture patterns (services, controllers, components, etc.)
- Design patterns used (factory, singleton, repository, etc.)
- Framework-specific conventions (NestJS modules, React hooks, etc.)
- Testing patterns
- Error handling patterns

**Why:** Ensures AI generates code that matches existing patterns and conventions

**Detection:** Scan codebase to identify:
- Backend: NestJS, Express, Django, Rails, Spring Boot, etc.
- Frontend: React, Vue, Angular, Next.js, etc.
- Languages: TypeScript, Python, Java, Go, Rust, etc.
- Patterns: Service layer, MVC, microservices, etc.

---

### 6. `standards.md`
**Purpose:** Code style, testing, git practices, performance standards
**Content:**
- Code formatting rules (ESLint, Prettier, Black, etc.)
- TypeScript/Python/Java rules (no `any`, type hints, etc.)
- Testing standards (coverage requirements, test types)
- Git practices (branch naming, commit messages, PR process)
- Performance standards (response times, query optimization)
- Dependency management (versioning, security updates)
- Code review standards

**Why:** Ensures consistent code quality and maintainability

---

## Optional Files (Generated If Applicable)

### 7. `integrations.md` (If external integrations exist)
**Purpose:** External services, APIs, third-party integrations
**Content:**
- External APIs used (REST, GraphQL, SOAP)
- Authentication methods (API keys, OAuth, etc.)
- Rate limits and quotas
- Error handling and retries
- Webhooks and event handling
- Integration-specific patterns

**When:** Detect from codebase (API clients, SDK usage, webhook handlers)

---

### 8. `monitoring.md` (If production monitoring exists)
**Purpose:** Logging, metrics, tracing, debugging
**Content:**
- Logging strategy (structured logs, log levels)
- Metrics and monitoring (Prometheus, Datadog, etc.)
- Tracing (distributed tracing, trace IDs)
- Error tracking (Sentry, Rollbar, etc.)
- Debugging practices
- Performance monitoring

**When:** Detect from codebase (logging libraries, metrics endpoints, monitoring tools)

---

### 9. `custom-instructions.md` (Always generated)

**Purpose:** User-defined instructions and preferences; fully editable by the user.
**Content:**
- Header telling the user they are free to add whatever they want (with examples)
- Placeholder examples of custom instructions (e.g. "When commenting code, explain WHY not WHAT")
- Bullet list for the user to add their own items

**Why:** Gives the user a single place to express preferences (tone, code style, process) that the assistant loads with project info. Not stable project truth — it's owned by the user.

**Generation:** Always create this file when generating project info. Use content from `/ai-rpi-protocol/core/project-info/custom-instructions-template.md`.

---

## File Naming Convention

**Format:** `kebab-case.md` (lowercase, hyphens)

**Rationale:**
- ✅ Works on all filesystems (Windows, Linux, macOS)
- ✅ URL-friendly
- ✅ Consistent with modern conventions
- ✅ Easy to type and remember

---

## Directory Structure

```
<repo-root>/
├── /ai-rpi-protocol/
└── /ai-rpi-protocol_project-info/
    ├── overview.md              # Core: Project overview
    ├── constraints.md           # Core: Non-negotiable rules
    ├── glossary.md              # Core: Domain terminology
    ├── structure.md             # Core: Structure & organization
    ├── stack-patterns.md        # Core: Stack-specific patterns
    ├── standards.md             # Core: Code quality standards
    │
    ├── integrations.md          # Optional: External services
    ├── monitoring.md            # Optional: Monitoring & debugging
    └── custom-instructions.md   # User preferences (always generated)
```

---

## Generation Order

1. **overview.md** (foundation)
2. **constraints.md** (safety first)
3. **structure.md** (structure understanding)
4. **stack-patterns.md** (pattern detection)
5. **glossary.md** (terminology extraction)
6. **standards.md** (quality standards)
7. **integrations.md** (if detected)
8. **monitoring.md** (if detected)
9. **custom-instructions.md** (always; user edits after generation)

---

## Detection Logic

**Stack Detection:**
- Scan `package.json`, `composer.json`, `requirements.txt`, `Cargo.toml`, `pom.xml`, etc.
- Look for framework indicators (NestJS, Express, Django, Rails, React, Vue, etc.)
- Detect language from file extensions and config files
- Identify architecture patterns from code structure

**Integration Detection:**
- Look for API client libraries
- Check for webhook handlers
- Find external service configurations
- Detect SDK usage

**Observability Detection:**
- Check for logging libraries (Winston, Pino, Log4j, etc.)
- Look for metrics endpoints (`/metrics`, Prometheus)
- Detect error tracking (Sentry, Rollbar)
- Find monitoring tool configurations

---

## Benefits of This Structure

✅ **Comprehensive:** Covers all essential project context
✅ **Modular:** Generate only what's needed
✅ **Stack-Agnostic:** Works for any project type
✅ **Stack-Specific:** Detects and adapts to actual stack
✅ **Maintainable:** Clear naming, logical organization
✅ **Extensible:** Easy to add more files if needed
